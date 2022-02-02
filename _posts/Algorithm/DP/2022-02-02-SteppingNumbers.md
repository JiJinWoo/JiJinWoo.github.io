---
layout: single
title: "[DP] Stepping Numbers.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;
const int MODE = pow(10,9)+7;

int topdown(int n, int i){
    if(n==1){
        if(i<=0 || i>9) return 0;
        else return 1;
    }
    if(dp[n][i]!=-1) return dp[n][i];
    dp[n][i] = (i-1>=0 ? topdown(n-1,i-1)%MODE : 0) + (i+1<=9 ? topdown(n-1,i+1)%MODE : 0);
    return dp[n][i]%MODE;
}

int solve(int n) {
    if(n==1) return 10;
    dp.clear();
    dp.resize(n+1,vector<int>(10,-1));
    long long res=0;
    for(int i=0; i<=9; i++){
        res+=topdown(n,i)%MODE;
        res%=MODE;
    }
    return res;
}
```