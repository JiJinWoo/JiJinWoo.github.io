---
layout: single
title: "[DP]Increasing Digits"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;
int topdown(int n, int i){
    if(n==1){
        if(i==0) return 0;
        else return 1;
    }
    if(dp[n][i]!=-1) return dp[n][i];
    
    int temp = 0;
    for(int k=0; k<i; k++){
        temp += topdown(n-1,k);
    }
    return dp[n][i] = temp;
}

int solve(int n) {
    dp.clear();
    dp.resize(n+1,vector<int>(10,-1));
    int res = 0;
    for(int i=0; i<=9; i++){
        res += topdown(n,i);
    }
    return res;
}
```