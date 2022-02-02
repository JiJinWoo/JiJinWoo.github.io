---
layout: single
title: "[String] Shortest String."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
int solve(string s) {
    int cnt = 0;
    for(char &c: s){
        cnt += (c=='1'?1:-1);
    }
    return abs(cnt);
}

```