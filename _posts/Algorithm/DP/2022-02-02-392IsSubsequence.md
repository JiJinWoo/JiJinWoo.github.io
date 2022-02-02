---
layout: single
title: "[DP]#392 Is Subsequence"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i=0, j=0;
        while(j<t.length()){
            if(t[j]==s[i])i++;
            j++;
        }
        cout<<i<<" "<<j;
        if(i<s.length()) return false;
        return true;
    }
};
```