---
layout: single
title: "[Tree] Left Side View of a Tree."
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

 //BFS Solution
vector<int> solve(Tree* root) {
    vector<int>res;
    queue<Tree*>Q;
    Q.push(root);

    while(!Q.empty()){
        int size = Q.size();
        res.push_back(Q.front()->val);
        for(int i=0; i<size; i++){
            auto cur = Q.front(); Q.pop();
            if(cur->left) Q.push(cur->left);
            if(cur->right) Q.push(cur->right);
        }
    }
    
    return res;
}

// DFS Solution
void dfs(Tree* root, vector<int>&res, int level){
    if(!root) return;
    if(level==res.size()) res.push_back(root->val);
    dfs(root->left,res,level+1);
    dfs(root->right,res,level+1);
}

vector<int> solve(Tree* root) {
    vector<int>res;
    dfs(root,res,0);
    return res;
}
```