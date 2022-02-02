---
layout: single
title: "[DFS] DFS&Recursion #112 Path Sum."
categories: ["bfsdfs"]
tag: [algorithm, dfs, leetcode]
---
```cpp

class Solution {
public:
     bool hasPathSum(TreeNode* root, int sum) {
        if(!root)return false;
         if(!root->left && !root->right && sum==root->val) return true;
         return hasPathSum(root->left, sum-root->val) ||  hasPathSum(root->right, sum-root->val);

    }
/*  bool istrue=false;
    int global_sum;
   void pathsum(TreeNode* root, int sum){
       if(!root)return;
       sum+=root->val;
       if(!root->left && !root->right){
           if(sum==global_sum){
               istrue=true;
               return;
           }
           else return;
       }
       pathsum(root->left,sum);
       pathsum(root->right,sum);
       
       
   }
    bool hasPathSum(TreeNode* root, int sum) {
        global_sum=sum;
        pathsum(root,0);
        return istrue;

    }*/
};
```