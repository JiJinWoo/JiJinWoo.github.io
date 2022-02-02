---
layout: single
title: "[String] Longest Anagram Subsequence."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
int solve(string a, string b) {
    unordered_map<char,int>mp;
    int res = 0;
    for(char &c: a) mp[c]++;
    for(char &c: b){
        if(--mp[c]>=0) res++;
    }
    return res; 
}

```