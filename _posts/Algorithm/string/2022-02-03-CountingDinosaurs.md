---
layout: single
title: "[String] Counting Dinosaurs."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
int solve(string animals, string dinosaurs) {
    int cnt = 0;
    unordered_set<char>st;
    for(auto c: dinosaurs)
        st.insert(c);
    for(auto c: animals)
        if(st.count(c)) cnt++; 
    return cnt;
}
```