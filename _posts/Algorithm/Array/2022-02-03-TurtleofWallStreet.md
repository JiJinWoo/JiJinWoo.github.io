---
layout: single
title: "[Array] Turtle of Wall Street."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(vector<int>& nums) {
    int n = nums.size();
    if(n==0) return 0;
    int cur_max = nums[n-1];
    int res = 0, profit;

     for(int i=n-1; i>=0; i--){
        cur_max = max(cur_max,nums[i]);
        profit = cur_max - nums[i];
        res += (profit > 0 ? profit : 0);
    }

    return res;
    
}
```