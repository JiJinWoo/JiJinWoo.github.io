---
layout: single
title: "[Tree] Longest Even Value Path."
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
int max_len;

int dfs(Tree* root){
    if(!root) return 0;
    int left = dfs(root->left);
    int right = dfs(root->right);
    if(root->val%2 & 1) return 0;
    max_len = max(max_len,1+left+right);
    return max(left,right)+1;
}

int solve(Tree* root) {
    max_len = INT_MIN;
    dfs(root);
    return max_len;
}
```