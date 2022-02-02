---
layout: single
title: "[String] Consecutively Descending Integers."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
bool solve(string s) {
    int n = s.length();
    if(n==1) return false;
    int prev, next, digit;
    bool temp = true;
    for(int i=1; i<n; i++){
        temp = true;
        next = stoi(s.substr(0,i))-1;
         
        for(int j=i; j<n; j+=to_string(next+1).length()){
            digit = to_string(next).length();
            if(s.substr(j,digit) != to_string(next)){
                temp = false;
                break;
            }
            next = next-1;
        }
        if(temp) return true;
    }
    return false;
}
```