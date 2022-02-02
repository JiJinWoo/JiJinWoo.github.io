---
layout: single
title: "[Array] Big Numbers."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();
    vector<int>row(n,INT_MIN), col(m,INT_MIN);
    int res = 0;

   for(int i=0; i<n; i++){
       for(int j=0; j<m; j++){
           row[i] = max(row[i], matrix[i][j]);
           col[j] = max(col[j], matrix[i][j]);
       }
   }

   for(int i=0; i<n; i++)
       for(int j=0; j<m; j++) 
            res += (matrix[i][j]==row[i] && matrix[i][j]==col[j]);
   

    return res;
}
```