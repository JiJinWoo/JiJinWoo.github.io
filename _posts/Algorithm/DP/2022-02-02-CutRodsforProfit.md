---
layout: single
title: "[DP]Cut Rods for Profit"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;
int unit_profit;
int cut_cost;

// dp[i][j] = 0-i까지 rods들을 이용해서 j length인 rod만을 팔아서 얻을수 있는 max profit
int topdown(vector<int>&rods, int i, int j){ 
    if(i < 0) return 0;
    if(rods[i] < j) return dp[i][j] = 0;
    if(rods[i]==j) dp[i][j] = rods[i] * unit_profit + topdown(rods,i-1,j);
    if(dp[i][j] != INT_MIN) return dp[i][j];
    
    dp[i][j] = max(topdown(rods,i-1,j),((rods[i]/j) * j * unit_profit - ((rods[i]-1)/j)*cut_cost) + topdown(rods, i-1, j));
    return dp[i][j];
}

int solve(vector<int>& rods, int p, int c) {
    if(rods.size()==0) return 0;
    sort(rods.begin(), rods.end());
    int n = rods.size();
    
    dp = {};
    dp.resize(n,vector<int>(rods[n-1]+1,INT_MIN));
    unit_profit = p;
    cut_cost = c;

    int res = 0;
    for(int j=1; j<=rods[n-1]; j++)
        res = max(res, topdown(rods,n-1, j));
    
    return res;
}

```