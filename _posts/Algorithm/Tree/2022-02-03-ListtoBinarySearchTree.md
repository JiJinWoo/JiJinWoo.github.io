---
layout: single
title: "[Tree] List to Binary Search Tree."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
/**
 * class Tree {
 *     public:
 *         int val;
 *         Tree *left;
 *         Tree *right;
 * };
 */
Tree* help(vector<int>&nums, int i, int j){
    if(i>j) return NULL;
    if(i==j) return new Tree(nums[i]);
    
    int m = i+(j-i+1)/2;
    Tree* node = new Tree(nums[m]);
    node->left = help(nums,i,m-1);
    node->right = help(nums,m+1,j);
    return node;
}
Tree* solve(vector<int>& nums) {
    return help(nums,0,nums.size()-1);
}
```