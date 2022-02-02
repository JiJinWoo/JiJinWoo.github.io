---
layout: single
title: "[DP]Shortest Common Supersequence"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;

int topdown(string &a, string &b, int i, int j){
    if(i<0 && j<0) return 0;
    if(i<0) return j+1;
    if(j<0) return i+1;
    if(dp[i][j]!=INT_MAX) return dp[i][j];

    if(a[i]==b[j]) dp[i][j] = 1 + topdown(a,b,i-1,j-1);
    else dp[i][j] = 1+min(topdown(a,b,i-1,j),topdown(a,b,i,j-1));
    return dp[i][j];
}

int solve(string a, string b) {
    int n = a.length(), m = b.length();
    dp={};
    dp.resize(n,vector<int>(m,INT_MAX));
    return topdown(a,b,n-1,m-1);
}
```