---
layout: single
title: "[DP]Poly Knapsack"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//1D DP
vector<int>dp;
int n;
int topdown(vector<int>&w, vector<int>&v, int c){
    if(c<=0) return 0;
    if(dp[c]!=-1) return dp[c];
    for(int i=0; i<n; i++){
        if(w[i]<=c){
            dp[c] = max(dp[c],v[i]+topdown(w,v,c-w[i]));
        }
    }
    return dp[c]==-1?0:dp[c];
}
int solve(vector<int>& w, vector<int>& v, int c) {
    n = w.size();
    dp.clear();
    dp.resize(c+1,-1);
    return topdown(w,v,c);
}

//2D DP
vector<vector<int>>dp;
int n;
int topdown(vector<int>&w, vector<int>&v, int c, int i){
    if(c<=0 || i<0) return 0;
    if(dp[i][c]!=-1) return dp[i][c];
   if(w[i]>c) dp[i][c] = topdown(w,v,c,i-1);
   else{
       dp[i][c] = max({topdown(w,v,c,i-1),v[i]+topdown(w,v,c-w[i],i-1),v[i]+topdown(w,v,c-w[i],i)});
   }
    return dp[i][c];
}
int solve(vector<int>& w, vector<int>& v, int c) {
    n = w.size();
    dp.clear();
    dp.resize(n,vector<int>(c+1,-1));
    return topdown(w,v,c,n-1);
}
```