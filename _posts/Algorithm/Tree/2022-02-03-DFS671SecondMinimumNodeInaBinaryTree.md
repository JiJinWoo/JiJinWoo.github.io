---
layout: single
title: "[Tree] DFS #671 Second Minimum Node In a Binary Tree."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

class Solution {
public:
    int min_of_mins = INT_MAX;
    int rootVal;
    void minfunc(TreeNode* root){
        if(!root) return;
        if(!root->left && !root->right){
            if(root->val == rootVal) return;
            min_of_mins = min(min_of_mins,root->val);
            return;
        }
        minfunc(root->left);
        minfunc(root->right);
    }

    bool isUni(TreeNode* root, int x){
        if(!root)return true;
        if(root->val != x) return false;
        return isUni(root->left, root->val) && isUni(root->right, root->val);
        
    }
    int findSecondMinimumValue(TreeNode* root) {
        if(isUni(root,root->val)) return -1;
        rootVal = root->val;
        minfunc(root);
        return min_of_mins;
    }
};
```