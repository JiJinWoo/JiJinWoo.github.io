---
layout: single
title: "[Array] Merging K Sorted Lists."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(vector<vector<int>>& lists) {
    priority_queue<int,vector<int>, greater<int>>pq;
    for(auto list: lists)
        for(auto element: list)
            pq.push(element);
    
    vector<int>res;
    while(!pq.empty()){
        res.push_back(pq.top());
        pq.pop();
    }
    return res;
}
```