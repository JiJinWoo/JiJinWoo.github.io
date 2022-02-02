---
layout: single
title: "[Tree] DFS&Recursion #687 Longest Univalue Path."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

class Solution {
public:
    int mx = INT_MIN;
 int path(TreeNode* root){
   int l = root->left ? path(root->left):0;
   int r = root->right ? path(root->right):0;
    
     l = (root->left && root->val == root->left->val) ? l+1 : 0;
     r = (root->right && root->val == root->right->val) ? r+1 : 0;
     
     mx = max(mx,l+r);
     return max(l,r);
        
 }
    
    int longestUnivaluePath(TreeNode* root) {
        if(!root) return 0;
        path(root);
        return mx;
    }
};
```