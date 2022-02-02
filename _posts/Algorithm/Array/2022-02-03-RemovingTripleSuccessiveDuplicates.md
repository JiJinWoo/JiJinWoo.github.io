---
layout: single
title: "[Array] Removing Triple Successive Duplicates."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(string s) {
    int zero = 0;
    int one = 0;
    int n = s.length();
    int res = 0;

    for(int i=0; i<n; i++){
        if(s[i] == '0'){
            one=0;
            if(++zero == 3){
                if(i<n-1 && s[i+1]=='1'){
                    s[i-1] = '1';
                    one = 0;
                }else{
                s[i] = '1';
                one = 1;
                }
                zero = 0;
                res++;
            }
        }else{
            zero=0;
            if(++one == 3){
                if(i<n-1 && s[i+1]=='0'){
                    s[i-1] = '0';
                    zero = 0;
                }else{
                s[i] = '0';
                zero = 1;
                }
                one = 0;
                res++;
            }
        }
    }

    return res;
}
```