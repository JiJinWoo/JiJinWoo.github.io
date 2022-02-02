---
layout: single
title: "[Tree] Binary Tree Width."
categories: ["tree"]
tag: [algorithm, tree, leetcode]
---
```cpp

int solve(Tree* root) {
   queue<pair<Tree*,int>>Q;
   Q.push({root,1});
   int res = 0, size, k, l, r;
   Tree* node;

   while(!Q.empty()){
       size = Q.size();
       l = INT_MAX; r = INT_MIN;

       for(int i=0; i<size; i++){
           node = Q.front().first;
           k = Q.front().second;
           Q.pop();

           l = min(l,k);
           r = max(r,k);
           res = max(res, r - l + 1);
           if(node->left) Q.push({node->left, 2*k - 1});
           if(node->right) Q.push({node->right, 2*k});
       }
   }

   return res;
}
```