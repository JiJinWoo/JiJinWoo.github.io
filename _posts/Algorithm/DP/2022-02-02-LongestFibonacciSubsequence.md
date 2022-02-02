---
layout: single
title: "[DP] Longest Fibonacci Subsequence."
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
int solve(vector<int>& nums) {
    int n = nums.size();
    unordered_map<int,int>mp;
    int res = 0;
    for(int i=0; i<n; i++) mp[nums[i]]=i;
    vector<vector<int>>dp(n,vector<int>(n,2));

    for(int i=0; i<n; i++){
        for(int j=0; j<i; j++){
            if(nums[i]-nums[j]<nums[j] && mp.count(nums[i]-nums[j])){
                dp[i][j] = max(dp[i][j], dp[j][mp[nums[i]-nums[j]]]+1);
                res = max(res,dp[i][j]);
            }
        }
    }
    return res<=2 ? 0 : res;
}

// nums[i] = nums[i-1] + nums[i-2];
// j     i
// 2 5 7 9 10 12

// 1 2 3 4 5

```