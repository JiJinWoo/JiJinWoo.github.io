---
layout: single
title: "[Array] Shortest Sublist to Sort."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(vector<int>& nums) {
    int n = nums.size();
    vector<int> sorted(nums);
    sort(sorted.begin(), sorted.end());
    vector<int>res;
    
    for(int i=0; i<n; i++){
        if(sorted[i]!=nums[i]) res.push_back(i);
    }
    if(res.size()==0) return 0;
    return res[res.size()-1]-res[0] + 1;
}
```