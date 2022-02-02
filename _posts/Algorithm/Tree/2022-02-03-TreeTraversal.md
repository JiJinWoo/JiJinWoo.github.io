---
layout: single
title: "[Tree] Tree Traversal."
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
unordered_map<Tree*,Tree*>parent;
void findParent(Tree* root, Tree* p){
    if(!root) return;
    if(p) parent[root] = p;
    findParent(root->left,root);
    findParent(root->right,root);
}

int solve(Tree* root, vector<string>& moves) {
    parent.clear();
    findParent(root,NULL);
    Tree* cur = root;
    for(string move: moves){
        if(move=="RIGHT"){
            cur = cur->right;
        }
        else if(move=="LEFT"){
            cur = cur->left;
        }
        else{ //UP
            cur = parent[cur];
        }
    }
    return cur->val;
}
```