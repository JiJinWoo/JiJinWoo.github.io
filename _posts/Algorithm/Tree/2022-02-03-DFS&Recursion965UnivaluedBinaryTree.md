---
layout: single
title: "[Tree] DFS&Recursion #965 Univalued Binary Tree."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

class Solution {
public:
   
    int unival;
    bool isUni(TreeNode* root){
        if(!root) return true;
        return root->val==unival && isUni(root->left)&&isUni(root->right);
    }
    bool isUnivalTree(TreeNode* root) {
        unival = root->val;
        return isUni(root);
        
        /*
     if(!root) return true;
        if(root->left&& root->left->val != root->val)return false;
        if(root->right && root->right->val !=root->val)return false;
        return isUnivalTree(root->left) && isUnivalTree(root->right);*/
        
    }
};
```