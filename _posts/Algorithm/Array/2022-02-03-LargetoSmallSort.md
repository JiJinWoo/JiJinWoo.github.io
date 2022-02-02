---
layout: single
title: "[Array] Large to Small Sort."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(vector<int>& nums) {
    int n = nums.size();
    vector<int>res;
    sort(nums.begin(), nums.end());
    int i = 0, j = n-1, flag = 0;
    while(i<=j){
        if(flag & 1) res.push_back(nums[i++]);
        else res.push_back(nums[j--]);
        flag++;
    }
    return res;
}


```