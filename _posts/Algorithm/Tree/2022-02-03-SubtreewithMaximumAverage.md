---
layout: single
title: "[Tree] Subtree with Maximum Average."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
double res;
double sum_root;
double num_root;
double avg;

pair<double,double>help(Tree* root){
    if(!root) return {0,0};
    pair<double,double>left = help(root->left);
    pair<double,double>right = help(root->right);
    sum_root = root->val + left.first + right.first;
    num_root = 1 + left.second + right.second;
    avg = sum_root/num_root;

    res = max(res, avg);
    return {sum_root,num_root};
}

double solve(Tree* root) {
    if(!root) return 0;
    res = INT_MIN;
    help(root);
    return res;
}
```