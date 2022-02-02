---
layout: single
title: "[Array] Interval Intersection."
categories: ["array"]
tag: [algorithm, array, leetcode]
---
```cpp
vector<int> solve(vector<vector<int>>& intervals) {
    vector<int> ret;
    ret.reserve(2);
    int maxStart = INT_MIN;
    int minEnd = INT_MAX;
    for (vector<int>& interval : intervals)
    {
        maxStart = max(interval[0], maxStart);
        minEnd = min(interval[1], minEnd);
    }
    ret.push_back(maxStart);
    ret.push_back(minEnd);
    return ret;

}
```