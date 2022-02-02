---
layout: single
title: "[Tree] Only Child."
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
int solve(Tree* root) {
    if(!root) return 0;
    return ((!root->left && root->right) || (root->left && !root->right)) + solve(root->left) + solve(root->right);
}
```