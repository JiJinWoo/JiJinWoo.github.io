---
layout: single
title: "[Array] Maximize Social Distancing."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
//link: https://binarysearch.com/problems/Maximize-Social-Distancing
int solve(vector<int>& seats) {
    int n = seats.size();
    int dist=0, max_dist = INT_MIN;
    int i=-1;
    for(int j=0; j<seats.size(); j++){
        if(seats[j]==1){
            if(i==-1) max_dist = max(max_dist,j);
            else max_dist = max(max_dist,(j-i)/2);  
            i = j;
        }
    }

    if(seats[n-1]==0) max_dist = max(max_dist,n-i-1);
    return max_dist;
}
```