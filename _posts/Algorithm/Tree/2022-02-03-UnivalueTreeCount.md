---
layout: single
title: "[Tree] Univalue Tree Count."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
int res;

bool help(Tree* root){
   if(!root) return true;
   bool isUni = help(root->left);
   isUni = help(root->right) && isUni;
   isUni = isUni && (root->left ? root->val==root->left->val : true) && (root->right ? root->val==root->right->val : true);
   if(isUni) res++;

   return isUni;
}

int solve(Tree* root) {
    res = 0;
    help(root);
    return res;
}
```