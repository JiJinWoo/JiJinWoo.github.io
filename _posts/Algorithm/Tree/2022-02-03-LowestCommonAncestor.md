---
layout: single
title: "[Tree] Lowest Common Ancestor."
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
int solve(Tree* root, int a, int b) {
    if(root==NULL) return INT_MIN;
    if(root->val == a or root->val == b) return root->val;
    int left = solve(root->left, a, b);
    int right = solve(root->right, a, b);
    if(left != INT_MIN and right != INT_MIN) return root->val;
    return left != INT_MIN ? left : right;
 }
```