---
layout: single
title: "[DP] Perfect Squares.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<int>dp;
int topdown(int n){
    if(n==1) return 1;
    if(n<1) return 0;
    if(dp[n]!=-1) return dp[n];
    int temp = INT_MAX, cnt = 1;
    while(cnt*cnt <= n){
        temp = min(temp, 1+topdown(n-cnt*cnt));
        cnt++;
    }
    return dp[n] = temp;
}
int solve(int n) {
    dp.clear();
    dp.resize(n+1,-1);
    return topdown(n);
}
```