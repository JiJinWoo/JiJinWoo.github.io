---
layout: single
title: "[Array] Squeezed List."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<vector<int>> solve(vector<int>& nums) {
    vector<vector<int>>res;
    int n = nums.size();
    int s=0, e=n-1;
    int left=0, right=0;
    while(s<=e){
        nums[s]+=left;
        nums[e]+=right;
        vector<int>sub{nums.begin()+s, nums.end()-(n-e-1)};
        left = nums[s++];
        right = nums[e--];
        
        res.push_back(sub);
    }
    if(n%2==0) res.push_back({left+right});
    
    return res;
}

```