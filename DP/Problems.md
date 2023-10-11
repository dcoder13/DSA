
# 1-D dp
<div>
<h2 > NOTE:</h2>
<h3> find all possible ways => recursion => memoiation</h3>
<h3>Try to represent problem in terms of index</h3>
<h3>Do all stuff at that index acc to the problem</h3>
<h3></h3>
</div>

## [Frog Jump](https://www.codingninjas.com/studio/problems/frog-jump_3621012)
- jump of 1 or 2 step size

### Using Memoiation:
```c++
#include <bits/stdc++.h>
int f(int n, vector<int> &h,vector<int>&dp)
{
    if(n==0)return 0;
    if(dp[n]!=-1)return dp[n];
    int one=f(n-1,h,dp) + abs(h[n]-h[n-1]);
    if(n>1)
    {
        return dp[n]=min(one , f(n-2,h,dp) + abs(h[n]-h[n-2]));
    }
    else return dp[n]=one;
}
int frogJump(int n, vector<int> &h)
{
    vector <int> dp(n,-1);
    return f(n-1,h,dp);
}
```
#### Analysis:
- **Time - O(N )**  
- **Space - O(N)`recursion stack` + O(N)`dp array`**
### Using Tabulation + Space Optimization:
```c++
#include <bits/stdc++.h>
  
int frogJump(int n, vector<int> &h)
{
    int dp1=0 , dp2;
    for(int i = 1 ; i < n ; i++)
    {
        int one = dp1 + abs(h[i]-h[i-1]);
        int two = INT_MAX;
        if(i>1)two = dp2 + abs(h[i]-h[i-2]);
        dp2=dp1;
        dp1=min(one,two);
    }
    return dp1;
}
```
#### Analysis:
- **Time - O(N)**  
- **Space - O(1)**

---
## [Frog Jump (k jump size)]()
### Memoiation :
```c++
int f(int n , int k , int dp[] , vector<int> &h)
{
    if(n==0)return 0;
    if(dp[n]!=-1)return dp[n];
    for(int i = 1 ; i <= k && i <=n ; i++)
    {
        if(dp[n]!=-1)
        {
            dp[n]=min(dp[n],f(n-i,k,dp,h) + abs(h[n]-h[n-i]));
  
        }
        else    
        dp[n]=f(n-i,k,dp,h) + abs(h[n]-h[n-i]);
    }
    return dp[n];
}
  
int minimizeCost(int n, int k, vector<int> &h){
    int dp[n];
    memset(dp,-1,sizeof(dp));
    return f(n-1,k,dp,h);
}
```

#### Analysis:
- **Time - O(N * K)**  
- **Space - O(N)`recursion stack` + O(N)`dp array`**

### Tabulation:
```c++

int minimizeCost(int n, int k, vector<int> &h){
    int dp[n];
    dp[0]=0;
  
    for(int i = 1 ; i < n ; i++)
    {
        dp[i]=abs(h[i]-h[i-1])+ dp[i-1];
        for(int j = 2 ; j <= k && j<=i ; j++)
        {
            dp[i]=min(dp[i],abs(h[i]-h[i-j])+ dp[i-j]);
        }
    }
    return dp[n-1];
}
```
#### Analysis:
- **Time - O(N * K)**  
- **Space - O(N)`dp array`**

### Space Optimization:
- No need , even if we make a dp array of O(K) space , it could be possible if N=K

---
---
## [House Robber(non consecutive selection-return max sum)](https://leetcode.com/problems/house-robber/)
---
### Memoiation:
```c++
class Solution {
public:
    int f(int n,vector<int> &v , int dp[])
    {
        if(n==0)return 0;
        if(n==1)return v[n-1];
        if(dp[n]!=-1)return dp[n];
        int pick = f(n-2,v,dp) + v[n-1];
        int pass=f(n-1,v,dp);
        return dp[n]=max(pick,pass);
    }
    int rob(vector<int>& v) 
    {
        int dp[v.size()+1];
        memset(dp,-1,sizeof(dp));
        return f(v.size(),v,dp);
        
    }
};
```
#### Analysis:
- **Time - O(N)**  
- **Space - O(N)`recursion stack` + O(N)`dp array`**
### Tabulation
```c++
class Solution {
public:
    
    int rob(vector<int>& v) 
    {
        int dp[v.size()+1];
        memset(dp,-1,sizeof(dp));
        int dp1=0;
        int dp2=v[0];
        for(int i = 2 ; i <= v.size() ; i++)
        {
            int pick = v[i-1] + dp1;
            int leave=dp2;
            dp1=dp2;
            dp2=max(pick,leave);

        }
        return dp2;
    }
};
```
#### Analysis:
- **Time - O(N)**  
- **Space -  O(N)`dp array`**
### Space Optimization
```c++
public:
    
    int rob(vector<int>& v) 
    {
        int dp1=0;
        int dp2=v[0];
        int pick,leave;
        for(int i = 2 ; i <= v.size() ; i++)
        {
            pick = v[i-1] + dp1;
            leave=dp2;
            dp1=dp2;
            dp2=max(pick,leave);

        }
        return dp2;
    }
};
```
#### Analysis:
- **Time - O(N * K)**  
- **Space - O(1)**


---
## [House Robber II (circular)](https://leetcode.com/problems/house-robber-ii/)
### Memoiation:
```c++
class Solution {
public:
    int f1(int n , int dp[],vector<int>&v)
    {
        if(n<=1)return 0;
        if(dp[n]!=-1)return dp[n];
        int pick = f1(n-2,dp,v) + v[n-1];
        int leave= f1(n-1,dp,v);
        return dp[n]=max(pick,leave);
    }
    int f2(int n , int dp[] , vector <int> &v)
    {
        if(n==0)return 0;
        if(n==1)return v[0];
        if(dp[n]!=-1)return dp[n];
        int pick = f2(n-2,dp,v) + v[n-1];
        int leave= f2(n-1,dp,v);
        return dp[n]=max(pick,leave);
    }
    int rob(vector<int>& v) {
        if(v.size()==1)return v[0];
        int dp[v.size()+1];
        memset(dp,-1,sizeof(dp));
        int ans=f1(v.size(),dp,v);
        memset(dp,-1,sizeof(dp));
        return max(ans,f2(v.size()-1,dp,v));
    }
};
```

### Tabulation + Space Optimization:
```c++
class Solution {
public:
    int f1(int n ,vector<int>&v)
    {
        int dp1=0;
        int dp2=0;
        for(int i = 1 ; i < n ; i++)
        {
            int pick = dp1 + v[i];
            int leave= dp2;
            dp1=dp2;
            dp2=max(pick,leave);
        }
        
        return dp2;
    }
    int f2(int n , vector <int> &v)
    {
        int dp1=0;
        int dp2=v[0];
        for(int i = 1 ; i < n-1 ; i++)
        {
            int pick = dp1 + v[i];
            int leave= dp2;
            dp1=dp2;
            dp2=max(pick,leave);
        }
        
        return dp2;
    }
    int rob(vector<int>& v) {
        if(v.size()==1)return v[0];
        return max(f1(v.size(),v),f2(v.size(),v));
    }
};
```
s