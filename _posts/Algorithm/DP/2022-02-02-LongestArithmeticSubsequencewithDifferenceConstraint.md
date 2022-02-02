---
layout: single
title: "[DP] Longest Arithmetic Subsequence with Difference Constraint.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
int solve(vector<int>& nums, int diff) {
    int n = nums.size();
    if(n==0) return 0;
    unordered_map<int,int>dp;
    int res = 1;

    for(int i=0; i<n; i++){
        if(dp.count(nums[i]-diff)){
            dp[nums[i]] = dp[nums[i]-diff] + 1;
            res = max(res, dp[nums[i]]);
        }else{
            dp[nums[i]] = 1;
        }
    }
}






```