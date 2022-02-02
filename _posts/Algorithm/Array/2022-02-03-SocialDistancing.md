---
layout: single
title: "[Array] Social Distancing."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(string s, int k) {
    int n = s.length(), prevX = -1, maxDist = 0;

    for(int i=0; i<n; i++){
        if(s[i]=='.') continue;
        if(prevX == -1) maxDist = i;
        else maxDist = max(maxDist, (i - prevX) / 2);
        prevX = i;
    }

    if(s[n-1] == '.') maxDist = max(maxDist,n-prevX-1);

    return maxDist >= k;
}
```