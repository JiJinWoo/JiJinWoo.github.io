---
layout: single
title: "[DP]maximum sum increasing subsequence"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
class Solution {
public:
    static bool compare(vector<int>a, vector<int>b){
        return a[0]*a[1] > b[0]*b[1] ? true : false;
    }
    
    int maxEnvelopes(vector<vector<int>>& env) {
        int n = env.size();
        if(n==0) return 0;
        sort(env.begin(), env.end(), compare);
        vector<int>dp(n,1);
        
        for(int i=1; i<n; i++)
            for(int j=0; j<i; j++)
                if(env[i][0]<env[j][0] && env[i][1]<env[j][1] && dp[j]+1>dp[i])
                    dp[i] = dp[j] + 1;
            
        return *max_element(dp.begin(),dp.end());
    }
};
```