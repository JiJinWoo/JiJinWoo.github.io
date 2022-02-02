---
layout: single
title: "[DP] #64 Minimum Path Sum (Leetcode/Medium)"
categories: ["dp"]
tag: [algorithm, dp]
---

```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size();
        if(n==0) return 0;
        int m = grid[0].size();
        vector<vector<int>>dp (n,vector<int>(m,INT_MAX));
        dp[0][0]=grid[0][0];
        for(int i=0; i<n; i++){
            for(int j=0; j<m; j++){
                if(i==0 && j==0) continue;
                if(i==0) {
                    dp[i][j]=dp[i][j-1]+grid[i][j];
                    continue;
                }
                if(j==0){
                    dp[i][j]=dp[i-1][j]+grid[i][j];
                    continue;
                }
               dp[i][j]=grid[i][j]+min(dp[i-1][j],dp[i][j-1]);
            }
        }
        return dp[n-1][m-1];
    }

};
```
