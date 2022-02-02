---
layout: single
title: "[DP] Minimum Sum Subsequence three consecutive."
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp

int solve(vector<int>& nums) {
   int n = nums.size();
   if(n==1) return nums[0];
   if(n==2) return min(nums[0],nums[1]);
   if(n==3) return min({nums[0],nums[1],nums[2]});

   vector<long>dp(n,0);
   dp[0]=nums[0], dp[1]=nums[1], dp[2]=nums[2];
   for(int i=3; i<n; i++){
       dp[i] = nums[i] + min({dp[i-1],dp[i-2],dp[i-3]});
   }

   return min({dp[n-1],dp[n-2],dp[n-3]});
}




```