---
layout: single
title: "[DP]Largest Elements in Their Row and Column"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
int solve(vector<vector<int>>& matrix) {
    int n = matrix.size(), m = matrix[0].size();
    vector<int>row(n,0),col(m,0);
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            row[i] += matrix[i][j];
            col[j] += matrix[i][j];
        }
    }

    int res=0;
    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            if(matrix[i][j]==1 && row[i]==1 && col[j]==1) res++;
        }
    }

    return res;
}
```