---
layout: single
title: "[Tree] Most Frequent Subtree Sum."
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
int res;
int most_freq;
unordered_map<int,int>mp;
int help(Tree* root){
    if(!root) return 0;
    int sum = root->val + help(root->left) + help(root->right);
    // cout<<sum<<" ";
    if(++mp[sum]>most_freq){
        most_freq = mp[sum];
        res = sum;
        // cout<<res<<" ";
    }
    return sum;
}
int solve(Tree* root) {
    res=0;
    most_freq = 0;
    mp.clear();
    help(root);
    return res;
}
```