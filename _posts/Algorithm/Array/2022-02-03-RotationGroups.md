---
layout: single
title: "[Array] Rotation Groups."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(vector<string>& words) {
    int n = words.size();
    int res = 0;
    unordered_set<string>st;

    for(string &word: words){
        if(st.count(word)) continue;
        else{
            for(int i=0; i<word.length(); i++){
                st.insert(word.substr(i)+word.substr(0,i));
            }
            res++;
        }
    }

    return res;
}
```