---
layout: single
title: "[DP] Delete Characters to Equalize Strings.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;

int topdown(string &a, string &b, int i, int j){
    if(i==-1 && j==-1) return 0;
    if(i==-1) return j+1;
    if(j==-1) return i+1;
    if(dp[i][j]!=-1) return dp[i][j];
    
    if(a[i]==b[j]) dp[i][j] = topdown(a,b,i-1,j-1);
    else dp[i][j] = 1+min(topdown(a,b,i-1,j),topdown(a,b,i,j-1));
    return dp[i][j];
}

int solve(string a, string b) {
    dp.clear();
    dp.resize(a.length(),vector<int>(b.length(),-1));
    return topdown(a,b,a.length()-1,b.length()-1);
}
```