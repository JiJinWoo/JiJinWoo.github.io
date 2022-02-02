---
layout: single
title: "[Tree] Second Place."
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
int first;
int second;

void help(Tree* root, int level){
    if(!root) return;
    if(!root->left && !root->right){
        if(level > first){
            second = first;
            first = level;
        }
        if(level>second && level<first) second = level;
    }
    
    help(root->left,level+1);
    help(root->right,level+1);
}

int solve(Tree* root) {
    first = INT_MIN;
    second = INT_MIN;
    help(root,0);
    return second;
}
```