---
layout: single
title: "[String] camelCase."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
string solve(vector<string>& words) {
    string res = "";
    for(int i=0; i<words.size(); i++){
        for(int j=0; j<words[i].length(); j++){
            if(i>=1 && j==0) words[i][j] = toupper(words[i][j]);
            else words[i][j] = tolower(words[i][j]);
            res+=words[i][j];
        }
    }
    return res;
}
```