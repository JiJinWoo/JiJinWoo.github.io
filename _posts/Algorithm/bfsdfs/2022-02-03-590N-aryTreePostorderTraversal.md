---
layout: single
title: "[DFS] #590 N-ary Tree Postorder Traversal."
categories: ["bfsdfs"]
tag: [algorithm, dfs, leetcode]
---
```cpp

class Solution {
public:
    vector<int> res;
    vector<int> postorder(Node* root) {
       stack<Node*>S;
        S.push(root);
        while(!S.empty()){
            if(!root) return {};
            auto cur = S.top(); S.pop(); res.push_back(cur->val);
            for(int i=0; i<cur->children.size(); i++)
                S.push(cur->children[i]);
        }
      
        reverse(res.begin(),res.end());
        return res;
    }
};
```