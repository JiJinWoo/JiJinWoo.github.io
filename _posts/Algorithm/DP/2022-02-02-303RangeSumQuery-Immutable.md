---
layout: single
title: "[DP] #303 Range Sum Query - Immutable."
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
class NumArray {
public:
    vector<int>dp{0};
    NumArray(vector<int>& nums) {
        int sum=0;
        for(int i: nums){
            sum+=i;
            dp.push_back(sum);
        }
    }
    
    int sumRange(int i, int j) {
        return dp[j+1]-dp[i];
        //dp[3]-dp[0]
        //dp[6]-dp[2];
    }
};
```