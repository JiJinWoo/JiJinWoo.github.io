---
layout: single
title: "[DP]Labyrinthian Possibilities"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//topdown
vector<vector<int>>dp;
int n,m;
#define MOD 1000000007
int topdown(vector<vector<int>>& matrix, int i, int j){
    if(i==0 && j==0) return 1;
    if(i<0 || i>=n || j<0 || j>=m || matrix[i][j]==1) return 0;
    if(dp[i][j]!=-1) return dp[i][j];
    return dp[i][j] = (topdown(matrix,i-1,j)%MOD+topdown(matrix,i,j-1)%MOD)%MOD;
}
int solve(vector<vector<int>>& matrix) {
    n = matrix.size(), m = matrix[0].size();
    dp.clear();
    dp.resize(n,vector<int>(m,-1));
    return topdown(matrix,n-1,m-1);
}


//bottom up
#define MOD 1000000007

int solve(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();
    vector<vector<int>>dp(n+1,vector<int>(m+1,0));
    dp[1][1] = 1;
    for(int i=1; i<=n; i++){
        for(int j=1; j<=m; j++){
            if(matrix[i-1][j-1]==1 || (i==1 && j==1)) continue;
            dp[i][j] = (dp[i-1][j] + dp[i][j-1])%MOD;
        }
        
    }

    return dp[n][m];
}
```