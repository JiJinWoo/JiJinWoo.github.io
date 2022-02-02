---
layout: single
title: "[Tree] Elephant Tree."
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
int dfs(Tree* root){
    if(!root) return 0;
    root->val += dfs(root->left) + dfs(root->right);
    return root->val;
}
Tree* solve(Tree* root) {
    dfs(root);
    return root;
}
```