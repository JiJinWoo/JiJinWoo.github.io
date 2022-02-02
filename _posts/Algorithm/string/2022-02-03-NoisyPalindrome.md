---
layout: single
title: "[String] Noisy Palindrome."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
bool solve(string s) {
    int n = s.length();
    int i = 0, j = n - 1;


    while(i<j){
        if(isdigit(s[i]) || isupper(s[i])){
            i++;
            continue;
        }
        else if(isdigit(s[j]) || isupper(s[j])){
            j--;
            continue;
        }
        else{
            if(s[i++]!=s[j--]) return false;
        }
    }
    return true;
}
```