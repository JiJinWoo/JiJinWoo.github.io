---
layout: single
title: "[Array] Text Editor."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
string solve(string s) {
    int n = s.size(); 
    string res="";
    int i=0;
    while(i<n){
        if(i<n-1 && s[i]=='<' && s[i+1]=='-'){
            if(!res.empty()) res.pop_back();
            i+=2;
        }else{
            res.push_back(s[i++]);
        }
    }
    return res;
}
```