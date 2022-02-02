---
layout: single
title: "[Array] Generate Anagram Substrings."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<string> solve(string s) {
    int n = s.length();
    string str;
    unordered_set<string>st;
    unordered_map<string,string>mp;
    vector<string>res;
    string sortedStr;
    for(int len=1; len<=n; len++){
        st.clear();
        for(int i=0; i<=n-len; i++){
            str = s.substr(i,len);
            sortedStr = str;
            sort(sortedStr.begin(), sortedStr.end());
            if(st.count(sortedStr)){
                res.push_back(str);
                if(mp.count(sortedStr)){
                    res.push_back(mp[sortedStr]); 
                    mp.erase(sortedStr);
                }
            }else{
                mp[sortedStr] = str;
            }
            st.insert(sortedStr);
        }
    }

    sort(res.begin(), res.end());

    return res;
}



```