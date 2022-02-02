---
layout: single
title: "[Array] Anagram Checks."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(string s0, string s1) {
    unordered_map<char,int>mp;
    for(char c: s0) mp[c]++;
    for(char c: s1){
        if(--mp[c]==0) mp.erase(c);
    }
    return mp.size()==0;
}
```