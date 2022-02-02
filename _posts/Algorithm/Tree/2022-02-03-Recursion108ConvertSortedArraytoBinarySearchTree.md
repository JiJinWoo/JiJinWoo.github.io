---
layout: single
title: "[Tree] Recursion #108 Convert Sorted Array to Binary Search Tree."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

class Solution {
public:
    
TreeNode* binarySearch(vector<int>& vec, int l, int r) {
    if(r<l) return NULL;     
   
     int m = l+(r - l) / 2;
     TreeNode* node = new TreeNode(vec[m]);
     node->left = binarySearch(vec, l, m - 1);
     node->right = binarySearch(vec, m + 1, r);
    
    return node;
}

    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return binarySearch(nums,0,nums.size()-1);
    }
};
```