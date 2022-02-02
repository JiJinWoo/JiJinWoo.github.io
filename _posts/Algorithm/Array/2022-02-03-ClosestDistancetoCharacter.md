---
layout: single
title: "[Array] Closest Distance to Character."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(string s, string c) {
    int n = s.length();
    int pos = 0;
    char t = c[0];
    vector<int>loc, res;
    
    for(int i=0; i<n; i++) 
        if(s[i]==t) loc.push_back(i);
    
    for(int i=0; i<n; i++){
        if(s[i]==t){
            res.push_back(0);
            if(i>0 && s[i]==s[i-1]) pos++;
            continue;
        }

        if((pos<loc.size()-1) && abs(loc[pos]-i)>=abs(loc[pos+1]-i)){
            res.push_back(abs(loc[pos+1]-i));
            pos++;
            continue;
        }
        res.push_back(abs(loc[pos]-i));
    }
    return res;
}

```