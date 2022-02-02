---
layout: single
title: "[DP] #698 Partition to K Equal Sum Subsets.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
class Solution {
private:
    int n;
public:
    bool dfs(vector<int>&nums, vector<int>&visited, int idx, int k, int currentSum, int target){
        if(k==1) return true;//Out of k sets, if we have found k-1 sets with 
				//equal sum, then the remaining one subset must have the equal sum

        if(currentSum == target) return dfs(nums,visited,0,k-1,0,target);

        for(int i=idx; i<n; i++){ //search all pairs
            if(visited[i] || currentSum + nums[i] > target) continue;
            visited[i]=true;
            if(dfs(nums,visited,i+1,k,currentSum+nums[i],target)) return true;
            visited[i]=false;
        }

        return false;
    }
    
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        n = nums.size();
        int total = accumulate(nums.begin(), nums.end(), 0);
        if(total%k!=0) return false;
        total/=k; //divide into k subsets so each subset has a sum of t/k
        vector<int>visited(n,false);
        
        return dfs(nums,visited,0,k,0,total);
    }
};
```