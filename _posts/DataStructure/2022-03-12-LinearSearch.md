---
layout: single
title: "[DS]LinearSearch"
categories: ["algorithm"]
tag: [datastructure]
author_profile: true
sidebar_main: true
---

> **LinearSearchAlgorithm 구현**

```cpp
#include<iostream>
using namespace std;

int linearSearch(int arr[], int len, int target){
    for(int i = 0; i < len; i++){
        if(target == arr[i]) return i;
    }
    return -1;
}

int main(){
    int arr[] = {2, 5, 8, 7, 9};
    int index = linearSearch(arr, sizeof(arr) / sizeof(int), 8);
    if(index == -1) cout << "false\n";
    else cout << index << endl;
}
```