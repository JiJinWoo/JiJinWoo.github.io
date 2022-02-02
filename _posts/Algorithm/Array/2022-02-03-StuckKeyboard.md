---
layout: single
title: "[Array] Stuck Keyboard."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(string s, string t) {
    int n = s.length(), m = t.length();
    int i=0, j=0, cnt1, cnt2;
    char cur;
    while(i<n || j<m){
        if(s[i]!=t[j]) return false;
        cur = s[i];
        cnt1=0, cnt2=0;
        while(i<n && s[i]==cur){
            i++; cnt1++;
        }
        while(j<m && t[j]==cur){
            j++; cnt2++;
        }
        if(cnt2>cnt1) return false;
    }
    return true;
    
}
```