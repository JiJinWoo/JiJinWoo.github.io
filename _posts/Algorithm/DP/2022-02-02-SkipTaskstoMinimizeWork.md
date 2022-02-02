---
layout: single
title: "[DP] Skip Tasks to Minimize Work.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//Space Complexity: O(n^2) Topdown
vector<vector<int>>dp;
int topdown(vector<int> &nums, int i, int j){
    //Base case: i<0
    if(i<0) return 0;
    if(dp[i][j]!=-1) return dp[i][j];
    if(j==1){
        dp[i][j] = topdown(nums,i-1,0);
    }else{
        dp[i][j] = nums[i] + min(topdown(nums,i-1,0),topdown(nums,i-1,1));
    }

    return dp[i][j];
}
int solve(vector<int>& nums) {
    int n = nums.size();
    dp.clear();
    dp.resize(n,vector<int>(2,-1));
    return min(topdown(nums,n-1,1),topdown(nums,n-1,0));
}

//Space Complexity: O(n) Botom up
int solve(vector<int>& nums) {
    int n = nums.size();
    if(n<=1) return 0;

    vector<int>dp(n+1,0);
    dp[0] = 0;
    dp[1] = nums[0];

    for(int i=2; i<=n; i++){
        dp[i] = min(dp[i-1],dp[i-2]) + nums[i-1];
    }

    return min(dp[n],dp[n-1]);    
}
```