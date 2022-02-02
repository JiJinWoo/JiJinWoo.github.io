---
layout: single
title: "[Array] Maximize Binary String Score."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(string s) {
    int res = INT_MIN;
    int n = s.length();

    int left_ones = 0;

    for(int i=0; i<n-1; i++){
        left_ones += (s[i]=='1');
        res = max(res,i+1-left_ones-left_ones);
    }

    left_ones += (s[n-1] == '1');
    return res+left_ones-10000;
}
```