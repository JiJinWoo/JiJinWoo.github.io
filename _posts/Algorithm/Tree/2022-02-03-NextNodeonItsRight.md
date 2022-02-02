---
layout: single
title: "[Tree] Next Node on Its Right."
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

Tree* solve(Tree* tree, int target) {
    queue<Tree*>Q;
    Q.push(tree);
    int size;
    bool flag = false;

    while(!Q.empty()){
        size = Q.size();
        for(int i=0; i<size; i++){
            auto cur = Q.front(); Q.pop();
            if(flag) return cur;
            if(cur->val == target) flag = true;
            
            if(cur->left) Q.push(cur->left);
            if(cur->right) Q.push(cur->right);
        }
        flag = false;
    }    

    return NULL;
}
```