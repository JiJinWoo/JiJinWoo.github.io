---
layout: single
title: "[Tree] Leaves in Same Level."
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
int leaf_level;

bool help(Tree* root, int level){
    if(!root) return true;
    if(!root->left && !root->right){
        if(leaf_level == -1){
            leaf_level = level;
            return true;
        }
        return leaf_level == level;
    }

    return help(root->left,level+1) && help(root->right, level+1);
}


bool solve(Tree* root) {
    leaf_level = -1;
    return help(root,0);
    
}
```