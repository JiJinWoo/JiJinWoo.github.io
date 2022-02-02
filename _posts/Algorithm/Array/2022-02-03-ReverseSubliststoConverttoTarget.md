---
layout: single
title: "[Array] Reverse Sublists to Convert to Target."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(vector<int>& nums, vector<int>& target) {
    unordered_map<int,int>mp;
    int n = nums.size(), m = target.size();
    for(int &i: nums) mp[i]++;
    for(int &i: target){
        if(!mp.count(i)) return false;
        if(--mp[i]==0) mp.erase(i);
    }
    return mp.size() == 0;
}
```