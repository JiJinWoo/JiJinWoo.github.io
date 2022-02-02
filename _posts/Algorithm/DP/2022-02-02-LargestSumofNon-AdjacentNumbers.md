---
layout: single
title: "[DP] Largest Sum of Non-Adjacent Numbers."
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//Bottom Up - O(n)
int solve(vector<int>& nums) {
    int n = nums.size();
    vector<int>dp(n+2,0);
    for(int i=2; i<=n+1; i++)
        dp[i] = max(dp[i-1],nums[i-2]+dp[i-2]);
        
    return dp[n+1];
}
//Topdown - O(n)
vector<int>dp;
int topdown(vector<int>&nums, int i){
    if(i<0) return 0;
    if(dp[i]!=INT_MIN) return dp[i];
    dp[i] = max (nums[i]+topdown(nums,i-2), topdown(nums,i-1));
    return dp[i];
}

int solve(vector<int>& nums) {
    dp.clear();
    dp.resize(nums.size(),INT_MIN);
    return topdown(nums,nums.size()-1);
}
```