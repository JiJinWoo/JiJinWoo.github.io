---
layout: single
title: "[String] #6 ZigZag Conversion."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
class Solution {
public:
    string convert(string s, int numRows) {
        string res;
        if(s.length()==0) return "";
        if(numRows==1) return s;
        for(int i=0; i<numRows; i++){
            int temp = i;
            int pos=i; int pos2=2*numRows-i-2;
            if(i==0 || i==numRows-1){
            while(pos<s.length()){
                res+=s[pos];
                pos+=2*(numRows-1);
            } continue;
            
            }
            while(pos<s.length()||pos2<s.length()){
                if(pos<s.length()){
                res+=s[pos];
                pos+=2*(numRows-1);
                }
                if(pos2<s.length()){
                res+=s[pos2];
                pos2+=2*(numRows-1);
                }
                
            }
            
            
            
        }
        return res;
    }
};
```