---
layout: single
title: "[Array] Largest Pair of Points."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(vector<int>& nums, vector<int>& values) {
    int n = nums.size();
    int subMax = INT_MIN, addMax = INT_MIN;
    
    for(int i=0; i<n; i++){
        subMax = max(subMax, values[i]-nums[i]);
        addMax = max(addMax, values[i]+nums[i]);
    }
    return subMax + addMax;
}
```