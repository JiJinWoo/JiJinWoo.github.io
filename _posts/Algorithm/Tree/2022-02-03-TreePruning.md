---
layout: single
title: "[Tree] Tree Pruning."
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

Tree* solve(Tree* root) {
  if(!root) return NULL;
  root->left = solve(root->left);
  root->right = solve(root->right);
  if(root->val==0 && !root->left && !root->right) return NULL;
  return root;
}
```