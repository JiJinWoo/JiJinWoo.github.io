---
layout: single
title: "[Array] Mixed Sorting."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(vector<int>& nums) {
    int n = nums.size(), i = 0, j = 0;
    vector<int>even, odd;
    for(auto num: nums){
        if(num & 1) odd.push_back(num);
        else even.push_back(num);
    }
    sort(even.begin(), even.end());
    sort(odd.begin(), odd.end(), greater<int>());
    int evenSize = even.size(), oddSize = odd.size();
    for(auto &num: nums){
        if(num & 1){
            num = odd[i++];
        }else{
            num = even[j++];
        }
    }
    return nums;
}
```