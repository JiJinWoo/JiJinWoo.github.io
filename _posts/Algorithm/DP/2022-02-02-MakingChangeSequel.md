---
layout: single
title: "[DP] Making Change Sequel.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
int solve(vector<int>& coins, int amount) {
    int n = coins.size();
    vector<vector<int>>dp(n+1,vector<int>(amount+1,INT_MAX));
    for(int i=0; i<=n; i++) dp[i][0] = 0;
    for(int i=1; i<=n; i++){
        for(int j=1; j<=amount; j++){
            if(coins[i-1]>j) dp[i][j] = dp[i-1][j];
            else{
                if(dp[i][j-coins[i-1]]==INT_MAX) dp[i][j] = dp[i-1][j];
                else dp[i][j] = min(dp[i][j-coins[i-1]]+1, dp[i-1][j]);
            }
        }
    }
    return dp[n][amount]==INT_MAX?-1:dp[n][amount];

}
```