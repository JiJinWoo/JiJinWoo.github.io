---
layout: single
title: "[String] Unidirectional Word Search."
categories: ["string"]
tag: [algorithm, string, leetcode]
---
```cpp
bool solve(vector<vector<string>>& board, string word) {
    int n = board.size(), m = board[0].size();
    string temp_row="", temp_col="";
    vector<string>col(m,"");

    for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
            temp_row += board[i][j];
            col[j] += board[i][j];
        }
        if(temp_row.find(word) != std::string::npos) return true;
        temp_row = "";
    }

    for(auto &str: col){
        if(str.find(word) != std::string::npos) return true;
    }

    return false;
}
```