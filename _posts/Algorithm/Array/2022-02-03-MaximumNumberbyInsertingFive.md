---
layout: single
title: "[Array] Maximum Number by Inserting Five."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
int solve(int n) {
    if(n==0) return 50;
    int isPositive = (n >= 0);
    string num = to_string(abs(n));
    int len = num.size();
    int i;

    for(i = 0; i<len; i++){
        if(isPositive){
            if(num[i]-'0' < 5) break;
        }else{
            if(num[i]-'0' > 5) break;
        }
    }

    num.insert(i,"5");
    if(!isPositive) num = "-" + num;
    return stoi(num);

    
}
```