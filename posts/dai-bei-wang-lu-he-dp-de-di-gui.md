---
title: '带备忘录和dp的递归'
date: 2020-10-23 14:49:02
tags: [算法,DP]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(4).jpg.webp
isTop: false
---
#### 备忘录算法
```C/C++
#include <iostream>
#include <vector>

using namespace std;

int helper(vector<int> &m, int n);
int fib(int n);

int fib(int n)
{
    if(n < 1)
    {
        return 0;
    }
    vector<int> m(n + 1, 0);
    return helper(m, n);
}

int helper(vector<int>&m, int n)
{
    if(n == 1 || n == 2) 
    {
        return 1;
    }
    if (m[n] != 0)
    {
        return m[n];
    }
    m[n] = helper(m, n - 1) + helper(m, n - 2);
    return m[n];
} 

int main()
{
    int n;
    cin >> n;
    cout << fib(n);
    return 0;
}
```
#### dp数组迭代
```C/C++
#include <iostream>
#include <vector>

using namespace std;

int fib(int n);

int fib(int n)
{
    if(n < 1)
    {
        return 0;
    }
    vector<int> dp(n + 1, 0);
    dp[1] = dp[2] = 1;
    for (int i = 3; i <= n; i++) 
    {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}

int main()
{
    int n;
    cin >> n;
    cout << fib(n);
    return 0;
}
```
#### 空间优化
```C/c++
#include <iostream>

using namespace std;

int fib(int n);

int fib(int n)
{
    if (n == 1 || n == 2)
    {
        return 1;
    }
    int a, b, sum;
    a = b = 1;
    for (int i = 3; i <= n; i++) 
    {
        sum = a + b;
        a = b;
        b = sum;
    }
    return sum;
}

int main()
{
    int n;
    cin >> n;
    cout << fib(n);
    return 0;
}
```