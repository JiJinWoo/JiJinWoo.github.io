---
layout: single
title: "[String] Consecutive Duplicates."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
string solve(string s) {
    int n = s.length();
    s += (s[n-1]=='X'?'Y':'X');
    // s = (s[0]=='X'?'Y':'X') + s;
    n+=1;

    int cnt = 1;
    string res = "";
    for(int i=1; i<n; i++){
        if(s[i]!=s[i-1]){
            // cout<<s[i]<<" "<<s[i-1]<<" "<<i<<endl;
            res += s[i-1];
        }
    }
    // cout<<s;

    return res;
}


```