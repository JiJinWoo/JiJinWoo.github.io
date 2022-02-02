---
layout: single
title: "[String] Interleaved String."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
string solve(string s0, string s1) {
    int n = s0.length(), m = s1.length();
    int i = 0, j = 0;
    string res = "";
    while(i<n || j<m){
        if(i<n){
            if(j>=m){
                res += s0.substr(i);
                return res;
            }
            res += s0[i++];
        }
        if(j<m){
            if(i>=n){
                res += s1.substr(j);
                return res;
            }
            res += s1[j++];
        }
    }
    return res;
}
```