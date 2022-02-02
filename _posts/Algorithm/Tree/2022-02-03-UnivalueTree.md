---
layout: single
title: "[Tree] Univalue Tree."
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
bool dfs(Tree* root, int val){
    if(!root) return true;
    if(root->val != val) return false;
    return dfs(root->left,val) && dfs(root->right,val);
}
bool solve(Tree* root) {
    if(!root) return true;
    return dfs(root,root->val);
}
```