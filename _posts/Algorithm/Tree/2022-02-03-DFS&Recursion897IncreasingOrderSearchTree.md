---
layout: single
title: "[Tree] DFS&Recursion #897 Increasing Order Search Tree."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

class Solution {
public:
   TreeNode* pre=nullptr;
    void search(TreeNode* root){
        if(!root) return;
        search(root->right);
        root->right=pre;
        pre=root;
        TreeNode* tmp = root->left;
        root->left=NULL;
        search(tmp);
    }
  
    TreeNode* increasingBST(TreeNode* root) {
      search(root);
    return pre;
    }
};
```