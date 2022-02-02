---
layout: single
title: "[Tree] DFS&Recursion #257 Binary Tree Paths."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
class Solution {
public:
    vector<string>path;
    void pathway(TreeNode* root,string p){
        if(!root) return;
        if(!root->left && !root->right){
            p+=to_string(root->val);
            path.push_back(p);
            return;
        }
        p+=to_string(root->val)+"->";
        pathway(root->left,p);
        pathway(root->right,p);
        
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        if(!root) return path;
        string p="";
        //p+=root->val+"->";
        pathway(root,p);
        return path;
        
    }
};
```