---
layout: single
title: "[Array] Look and Say."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
string solve(int n) {
    if(n==1) return "1";
    string s = "11";
    string temp;
    int cnt;


    for(int i=2; i<n; i++){
        cnt = 0;
        temp = "";
        cnt++;
        for(int j=1; j<s.length(); j++){
            if(s[j]!=s[j-1]){
                temp += (cnt+'0');
                temp += s[j-1];
                if(j==s.length()-1){
                    temp += "1";
                    temp += s[j];
                }
                cnt = 1;
            }else{
                cnt++;
                if(j==s.length()-1){
                    temp += (cnt+'0');
                    temp += s[j];
                }
            }
        }
        s = temp;
    }

    return s;
    
}
```