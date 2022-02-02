---
layout: single
title: "[DP] Minimum Dropping Path Sum With Column Distance Constraint."
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>>dp;
int n,m;
int topdown(vector<vector<int>>& matrix, int i, int j){
    if(j<0 || j>=m) return 100000;
    if(i == n-1) return matrix[i][j];
    if(dp[i][j]!=INT_MIN) return dp[i][j];
    dp[i][j] = matrix[i][j] + min({topdown(matrix,i+1,j-1),topdown(matrix,i+1,j),topdown(matrix,i+1,j+1)});
    return dp[i][j];  
}
int solve(vector<vector<int>>& matrix) {
    n = matrix.size();
    m = matrix[0].size();
    dp.clear();
    dp.resize(n,vector<int>(m,INT_MIN));
    int res = INT_MAX;
    for(int i=0; i<m; i++){
        res = min(res,topdown(matrix,0,i));
    }

    return res;
}


```