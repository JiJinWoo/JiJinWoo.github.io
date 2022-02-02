---
layout: single
title: "[String] Validate Delivery Orders."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
bool solve(vector<string>& orders) {
    unordered_set<string>pickups;
    unordered_set<string>history;
    string order_num;

    for(string &order: orders){
        order_num = order.substr(1);
        if(order[0]=='P'){
            if(history.count(order_num)) return false;
            pickups.insert(order_num);
        }else{
            if(!pickups.count(order_num)) return false;
            pickups.erase(order_num);
        }
        history.insert(order_num);
    }

    return pickups.size()==0;
}
```