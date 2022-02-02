---
layout: single
title: "[DFS] DFS&Recursion #897 Increasing Order Search Tree."
categories: ["bfsdfs"]
tag: [algorithm, dfs, leetcode]
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