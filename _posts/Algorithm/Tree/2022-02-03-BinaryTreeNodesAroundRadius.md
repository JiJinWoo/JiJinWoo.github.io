---
layout: single
title: "[Tree] Binary Tree Nodes Around Radius."
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
unordered_map<Tree*,Tree*>mp;
Tree* targetNode;
void connect(Tree* root, Tree *parent, int &target){
    if(!root) return;
    if(root->val == target) targetNode = root;
    if(parent) mp[root] = parent;
    connect(root->left,root,target);
    connect(root->right,root,target);
}

vector<int> solve(Tree* root, int target, int radius) {
    //complete parent map
    mp.clear(); targetNode=NULL;
    connect(root,NULL,target);
    unordered_set<Tree*>visited;

    //result vector
    vector<int>res;

    //BFS
    queue<Tree*>Q;
    Q.push(targetNode);
    int size;
    while(!Q.empty()){
        size = Q.size();
        for(int i=0; i<size; i++){
            auto cur = Q.front(); Q.pop();
            visited.insert(cur); //mark visited
            if(radius==0){ //when radius==0, we have reached our destination
                res.push_back(cur->val);
            }

            if(cur->left && !visited.count(cur->left)) Q.push(cur->left);
            if(cur->right && !visited.count(cur->right)) Q.push(cur->right);
            if(mp.count(cur) && !visited.count(mp[cur])) Q.push(mp[cur]);
        }
        if(radius==0) break;
        radius--;
    }
    sort(res.begin(),res.end());
    return res;
}
```
