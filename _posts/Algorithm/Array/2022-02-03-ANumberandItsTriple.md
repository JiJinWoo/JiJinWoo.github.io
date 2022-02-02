---
layout: single
title: "[Array] A Number and Its Triple."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(vector<int>& nums) {
    unordered_set<int>st;
    for(int &e: nums){
        if(st.count(e*3) || (e%3==0 && st.count(e/3))) return true;
        st.insert(e);
    }
    return false;
}
```