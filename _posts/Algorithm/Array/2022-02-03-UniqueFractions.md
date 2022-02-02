---
layout: single
title: "[Array] Unique Fractions."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
static bool compare(vector<int>a, vector<int>b){
    
    if(a[0]/(double)a[1] >= b[0]/(double)b[1]) return false;
    else return true;
}

int gcd(int i, int j){
    if(j==0) return abs(i);
    return gcd(j,i%j);
}

vector<vector<int>> solve(vector<vector<int>>& fractions) {
    set<vector<int>>st;
    int GCD; 
    for(auto &f: fractions){
        GCD = gcd(f[0],f[1]);
        st.insert({f[0]/GCD,f[1]/GCD});
    }

    vector<vector<int>>res;
    for(auto &s: st){
        res.push_back({s[0],s[1]});
    }
    sort(res.begin(), res.end(), compare);
    return res;
}
```