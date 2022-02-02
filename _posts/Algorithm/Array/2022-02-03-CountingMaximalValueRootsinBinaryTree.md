---
layout: single
title: "[Array] Counting Maximal Value Roots in Binary Tree."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
//Solution 2 -> Using Pair -> SLower
pair<int,int>helper(Tree* root){
    if(!root) return {0, INT_MIN};
    auto left = helper(root->left);
    auto right = helper(root->right);
    int max_val = max({root->val, left.second, right.second});
    return {(root->val==max_val) + left.first + right.first, max_val};
}
int solve(Tree* root) {
    return helper(root).first;
}
```