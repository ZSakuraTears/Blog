---
title: '凑零钱问题'
date: 2020-10-23 14:45:52
tags: [算法,DP]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(7).jpg.webp
isTop: false
---
```C/C++
#include <iostream>
#include <vector>
#include <limits.h>
#define INT_MAX 2147483647;
using namespace std;

int coinchange(int coin, vector<int> &coins, int amount, vector<int> &bwl) 
{
    if (amount < 0) return -1;
    if (amount == 0) return 0;
    if (bwl[amount] != 0) return bwl[amount];
    int res, i, j, dp = 0, m;
    m = INT_MAX;
    j = 0;
    res = INT_MAX;
    while (j < coin) {
        i = coins[j];
        dp = coinchange(coin, coins, amount - i, bwl);
        if (dp == -1) {
            j++;
            continue;
        }
        if (res > 1 + dp) {
            res = 1 + dp;
        }
        j++;
    }
    if (res != m) {
        bwl[amount] = res;
    }
    else {
        bwl[amount] = -1;
    }
    return bwl[amount];
}

int coinChange(vector<int>& coins, int amount) 
{
    int coin = coins.size();
    vector<int> bwl(amount + 1, 0);
    return coinchange(coin, coins, amount, bwl);
}


int main() 
{
    vector<int> coins;
    int a, n, i = 0, amount, m;
    cin >> n;
    coins.clear();
    while (i < n) {
        cin >> a;
        coins.push_back(a);
        i++;
    }
    cin >> amount;
    m = coinChange(coins, amount);
    cout << m;
    return 0;
}

```

```C/C++
#include <iostream>
#include <limits.h>
#include <vector>
#define INT_MAX 2147483647;
using namespace std;

int coinChange(vector<int> &coins, int amount)
{
    vector<int> dp(amount + 1, amount + 1);
    dp[0] = 0;
    int i, j;
    for (i = 0; i < dp.size(); i++) 
    {
        for (j = 0; j < coins.size(); j++)
        {
            if (i < coins[j])
            {
                continue;
            }
            if (dp[i] > dp[i - coins[j]]) 
            {
                dp[i] = 1 + dp[i - coins[j]];
            }
        }
    }
    return (dp[amount] == amount + 1) ? -1 : dp[amount];
}

int main()
{
    vector<int> coins;
    int a, n, i = 0, amount, m;
    cin >> n;
    coins.clear();
    while (i < n)
    {
        cin >> a;
        coins.push_back(a);
        i++;
    }
    cin >> amount;
    m = coinChange(coins, amount);
    cout << m;
    return 0;
}
```