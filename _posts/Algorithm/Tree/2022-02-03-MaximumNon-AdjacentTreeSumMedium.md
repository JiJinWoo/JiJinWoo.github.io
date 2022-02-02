---
layout: single
title: "[Tree] Maximum Non-Adjacent Tree Sum Medium."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp
// #1

int helper(Tree* root, bool canUse){
    if(!root) return 0;
    if(canUse){
        return max(
            root->val + helper(root->left,false) + helper(root->right,false),
            helper(root->left, true) + helper(root->right, true)
        );
    }else{
        return helper(root->left, true) + helper(root->right, true);
    }
}
int solve(Tree* root) {
    //쓸수있다 vs 못쓴다
    return helper(root,true);   
}

// #2
pair<int,int> help(Tree* root){
    if(!root) return {0,0};
    auto leftChild = help(root->left);
    auto rightChild = help(root->right);

    return {
        root->val + leftChild.second + rightChild.second,
        max(leftChild.first, leftChild.second) + max(rightChild.first, rightChild.second)
    };
}
int solve(Tree* root) {
    //쓸수있다 vs 못쓴다
    pair<int,int> res = help(root);
    return max(res.first, res.second);
}
```