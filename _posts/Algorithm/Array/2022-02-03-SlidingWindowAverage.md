---
layout: single
title: "[Array] Sliding Window Average."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
class SlidingWindowAverage {
    public:
    deque<int>dq;
    int size;
    double cur_sum=0;
    SlidingWindowAverage(int window_size) {
        size = window_size;
    }

    double average(int val) {
        dq.push_back(val);
        if(dq.size()==size+1){
            cur_sum-=dq.front();
            dq.pop_front();
        }
        cur_sum+=val;
        return cur_sum/(double)dq.size();
    }
};
```