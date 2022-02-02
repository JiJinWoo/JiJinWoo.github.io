---
layout: single
title: "[Array] Domino Placement."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(int n, int m) {
    if(n==1) return m/2;
    if(m==1) return n/2;
    if(n%2==0 || m%2==0) return n*m/2;
    return solve(n,m-1) + solve(n,1);
}

```