---
layout: single
title: "[Array] Shortest Majority Substring."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(string s) {
    int n = s.length();
    int res = INT_MAX, temp;
    int count[26]{};
    for(int i=0; i<26; i++) count[i] = -1;
    
    for(int i=0; i<n; i++){
        temp = count[s[i]-'a'];
        if(temp != -1 && 3 > i-temp) res = min(res,i-temp+1);
        count[s[i]-'a'] = i;
    }

    return res == INT_MAX ? -1 : res;
}
```