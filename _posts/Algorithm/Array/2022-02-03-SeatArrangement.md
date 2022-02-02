---
layout: single
title: "[Array] Seat Arrangement."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
bool solve(int n, vector<int>& seats) {
    seats.push_back(0); seats.push_back(1);
    int len = seats.size();
    int temp=1, availableSeats = 0;
    for(int i=0; i<len; i++){
        if(seats[i]==1){
            availableSeats += (temp-1)/2;
            temp = 0;
        }else{
            temp++;
        }
    }

    return availableSeats >= n;
}

// #2
bool solve(int n, vector<int>& seats) {
    for(int i=0; i<seats.size(); i++){
        if(n==0) return true;
        if(seats[i]==1) continue;
        if((i>0&&seats[i-1]==1) || (i<seats.size()-1&&seats[i+1]==1)) continue;
        n--;
        seats[i] = 1;
    }
    return n==0;
}
```