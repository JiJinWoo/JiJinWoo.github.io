---
layout: single
title: "[DP] Contiguous Intervals.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
vector<vector<int>> solve(vector<int>& nums) {
    vector<vector<int>>res;
    sort(nums.begin(), nums.end());
    int n = nums.size();
    if(n==0) return {};

    nums.push_back(nums[n++-1]+2);
    int left = nums[0];
    
    for(int i=1; i<n; i++){
        if(nums[i]!=nums[i-1]+1){
            res.push_back({left,nums[i-1]});
            left = nums[i];
        }
    }
    return res;
}
```