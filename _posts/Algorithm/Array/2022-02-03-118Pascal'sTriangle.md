---
layout: single
title: "[Array] #118 Pascal's Triangle."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        if(numRows==0) return {};
        vector<vector<int>>res {{1}};
        for(int n=1; n<numRows; n++){
            vector<int>sub;
            sub.push_back(1);
            for(int i=1; i<n; i++)
                sub.push_back(res[n-1][i]+res[n-1][i-1]);
            sub.push_back(1);
            res.push_back(sub);
        }
        return res;
    }
};
```