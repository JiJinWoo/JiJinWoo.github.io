---
layout: single
title: "[DFS] DFS&Recursion #653 Two Sm IV - Input is  BST(unordered_set)."
categories: ["bfsdfs"]
tag: [algorithm, dfs, leetcode]
---
```cpp

class Solution {
public:
  unordered_set<int> st;
    
    bool findTarget(TreeNode* root, int k) {
      if(!root) return false;
        if(st.count(k-root->val)) return true;
        st.insert(root->val);
        return findTarget(root->left,k) || findTarget(root->right,k);
    }
};
```