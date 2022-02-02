---
layout: single
title: "[DP] Longest Common Substring.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp

int solve(string s, string t) {
    int n = s.length(), m = t.length();
    int res = 0;
    vector<vector<int>>dp(n+1,vector<int>(m+1,0));
    for(int i=1; i<=n; i++){
        for(int j=1; j<=m; j++){
            if(s[i-1]==t[j-1]){
                dp[i][j] = 1 + dp[i-1][j-1];
                res = max(res,dp[i][j]);
            }else{ //can be omitted
                dp[i][j] = 0;
            }
        }
    }
    return res;
}

```