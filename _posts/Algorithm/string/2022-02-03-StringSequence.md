---
layout: single
title: "[String] String Sequence."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
string solve(string s0, string s1, int n) {
    string r1 = s0, r2 = s1, res="";
    if(n==0) return r1;
    if(n==1) return r2;

    for(int i=2; i<=n; i++){
        res = i & 1 ? r1+r2 : r2+r1;
        r1 = r2;
        r2 = res;
    }
    
    return res;
}




```