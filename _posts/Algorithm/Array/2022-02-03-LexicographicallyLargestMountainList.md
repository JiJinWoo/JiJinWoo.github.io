---
layout: single
title: "[Array] Lexicographically Largest Mountain List."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(int n, int lower, int upper) {
 if (n > (upper-lower)*2+1) return {};
 int left=0,right=0;
 if(n <= upper - lower + 1){
     left = upper - 1;
     right = upper - (n - 2);
 }else{
     left = upper-(n-(upper-lower+1));
     right = lower;
 }

 vector<int>res;
 for(int i=left; i<=upper; i++) res.push_back(i);
 for(int i=upper-1; i>=right; i--) res.push_back(i);
 return res;

}

// 2 3 4 5 (6) 5 4 3 2
```