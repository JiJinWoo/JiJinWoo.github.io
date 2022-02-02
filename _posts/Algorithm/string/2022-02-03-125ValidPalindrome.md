---
layout: single
title: "[String] #125 Valid Palindrome."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
class Solution {
public:
    #define Q (('A'<=s[start] && s[start]<='Z') || ('a'<=s[start] && s[start]<='z') ||)
    #define R (('A'<=s[end] && s[end]<='Z') || ('a'<=s[end] && s[end]<='z'))
    bool isPalindrome(string s) {
        int n = s.length();
        if(n==0 || n==1) return true;
      int i=0; int j=n-1;
        while(i<j){
            while(isalnum(s[i])==false && i<j) i++;
            while(isalnum(s[j])==false && i<j) j--;
            if(toupper(s[i])!=toupper(s[j])) return false;
            i++; j--;
        }
        return true;
    }
};
```