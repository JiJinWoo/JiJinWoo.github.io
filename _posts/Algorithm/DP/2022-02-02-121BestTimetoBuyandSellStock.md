---
layout: single
title: "[DP] #121 Best Time to Buy and Sell Stock.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//Kadane's Algorithm
//Better solution 
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size()<=1) return 0;
        int mx=INT_MIN;
        int start = 0; int current_mx=0;
        
        for(int i=1; i<prices.size(); i++){
            current_mx += prices[i]-prices[i-1];
            if(current_mx<0) current_mx=0;
            mx = max(mx,current_mx);
        }
        return mx;
    }
};

//acceptable
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size()<=1) return 0;
        int mx=INT_MIN;
        int start = 0;
        int current_mx=0;
        for(int i=1; i<prices.size(); i++){
            int diff = prices[i]-prices[i-1];
            current_mx +=diff;
            if(current_mx<0) current_mx=0;
            if(current_mx>mx) mx = current_mx;
 
        }
        return mx;
    }
};
```