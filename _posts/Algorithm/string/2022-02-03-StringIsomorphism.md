---
layout: single
title: "[String] String Isomorphism."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
bool solve(string s, string t) {
    int n = s.length();
    unordered_map<char,char>mp1, mp2;

    for(int i=0; i<n; i++){
        if(!mp1.count(s[i])){
            mp1[s[i]] = t[i];
        }else{
            if(mp1[s[i]] != t[i]) return false;
        }
        if(!mp2.count(t[i])){
            mp2[t[i]] = s[i];
        }else{
            if(mp2[t[i]] != s[i]) return false;
        }
    }

    return true;
}
```