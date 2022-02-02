---
layout: single
title: "[Tree] Leftmost Deepest Tree Node."
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
void dfs(Tree* root, int level, pair<int,int>&deep){
    if(!root) return;
    if(level > deep.first){
        deep.second =  root->val;
        deep.first = level;
    }
    dfs(root->left, level+1,deep);
    dfs(root->right, level+1,deep);
}

int solve(Tree* root) {
    pair<int,int>deep={0,root->val};
    dfs(root,0,deep);
    return deep.second;
}


//BFS
int solve(Tree* root) {
    queue<Tree*>Q;
    Q.push(root);
    int res;
    while(!Q.empty()){
        int size = Q.size();
        res = Q.front()->val;
        for(int i=0; i<size; i++){
            auto cur = Q.front(); Q.pop();
            if(cur->left) Q.push(cur->left);
            if(cur->right) Q.push(cur->right);
        }
    }
    return res;
}
```