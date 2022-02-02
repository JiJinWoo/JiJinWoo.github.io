---
layout: single
title: "[DP]Sort String by Flipping"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
int solve(string s) {
    int n = s.length();
    if(n==0) return 0;
    vector<int>leftX(n,0), rightY(n,0);

    
    leftX[0] = (s[0] == 'y');
    rightY[n-1] = (s[n-1] == 'x');

    for(int i=1; i<n; i++){
        leftX[i] = leftX[i-1] + (s[i] == 'y');
        rightY[n-1-i] = rightY[n-i] + (s[n-1-i] == 'x');
    }
    
    int res = INT_MAX;
    for(int i=0; i<n; i++){
        res = min(res, leftX[i]+rightY[i+1]);
    }

    res = min({res,leftX[n-1],rightY[0]});
    return res == INT_MAX ? 0 : res;
}
```