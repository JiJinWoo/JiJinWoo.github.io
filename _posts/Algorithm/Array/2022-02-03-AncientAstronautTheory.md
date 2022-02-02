---
layout: single
title: "[Array] Ancient Astronaut Theory."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(string dictionary, string s) {
    int pre = INT_MIN;
    int n = dictionary.length();
    unordered_map<char,int>mp;

    for(int i=0; i<n; i++) mp[dictionary[i]] = i;

    for(char &c: s){
        if(!mp.count(c)) continue;
        if(mp[c] < pre) return false;
        pre = mp[c];
    }

    return true;
}
```