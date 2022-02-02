---
layout: single
title: "[DP] Make a Palindrome by Inserting Characters.cpp"
categories: ["dp"]
tag: [algorithm, dp]
---
```cpp
//Top Down
vector<vector<int>>dp;
int n;
int topdown(string &s, int i, int j){
   if(i>=j) return 0;
   if(dp[i][j]!=-1) return dp[i][j];

   if(s[i]==s[j]) dp[i][j] = topdown(s,i+1,j-1);
   else dp[i][j] = min({1+topdown(s,i+1,j),1+topdown(s,i,j-1), 2+topdown(s,i+1,j-1)});

   return dp[i][j];
}

int solve(string s) {
   n = s.length();
   dp.clear();
   dp.resize(n,vector<int>(n,-1));
   return topdown(s,0,n-1);
    
}

//Bottom Up
int solve(string s) {
   int n = s.length();
   vector<vector<int>>dp(n,vector<int>(n,0));
   for(int i=0; i<n-1; i++){
      dp[i][i+1] = s[i]!=s[i+1];
   }

   for(int len=3; len<=n; len++){
      for(int i=0; i<=n-len; i++){
         int j = i+len-1;
         if(s[i]==s[j]) dp[i][j] = dp[i+1][j-1];
         else dp[i][j] = min({1+dp[i+1][j],1+dp[i][j-1],2+dp[i+1][j-1]});
      }
   }

   return dp[0][n-1]; 
    
}
```