---
layout: single
title: "[Tree] Longest Tree Path."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
int res;
int help(Tree* root){
    if(!root) return 0;
    int left = help(root->left);
    int right = help(root->right);
    res = max(res,1+left+right);

    return 1 + max(left,right);
}

int solve(Tree* root) {
    res = 0;
    help(root);
    return res;
}
```