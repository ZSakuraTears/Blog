---
title: '斐波那契数列(递归)'
date: 2020-12-17 17:13:05
tags: [算法,递归,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(5).jpg.webp
isTop: false
---
### 题目
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。
<!-- more -->
答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。<br><br>

 

示例 1：

输入：n = 2
输出：1<br><br>
示例 2：

输入：n = 5
输出：5<br><br>
 

提示：

0 <= n <= 100<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
#### 方法1：递归
常规递归方法，然后愉快的超时
```C++
class Solution {
public:
    int fib(int n) {
        if (n == 0) return 0;
        if (n == 1 || n == 2) {
            return 1;
        }
        return fib(n - 1) + fib(n - 2);
    }
};
```
#### 方法2：带备忘录的递归（自顶向下）
可以把递归看成一颗树，自顶向下
在递归的过程中很多元素其实已经被访问过了，比如n = 20，求n = 19 + n = 18，求19的时候求n = 18 + n = 17，这里可以看到n = 18被求了两次，下面的元素还有更多次重复的所以一般的递归时间复杂度非常高。如果可以把每个元素的值记录下来，下次求的时候直接用时间可以减少很多。
```C++
class Solution {
public:
    vector<int> arr;

    int help(int n) {
        if (n == 0) return 0;
        if (n == 1 || n == 2) {
            return 1;
        }
        if (arr[n] != 0) { //如果已经记录则直接用
            return arr[n];
        }
        //未记录则记录下来
        arr[n - 1] = help(n - 1) % 1000000007;
        arr[n - 2] = help(n - 2) % 1000000007;
        return arr[n - 1] + arr[n - 2];
    }

    int fib(int n) {
        for (int i = 1; i <= 101; i++) {
            arr.push_back(0);
        }
        return help(n) % 1000000007;
    }
};
```
#### 方法3：DP（自底向上）
方法2是从树的顶端到下面依次递归求值，也可以从树的底端到顶端求。
还是利用一个数组，把每个值记录下来，从底到顶。
```C++
class Solution {
public:
    int fib(int n) {
        int dp[101];
        dp[1] = 1;
        dp[2] = 1;
        if (n == 0) {
            return 0;
        }
        if (n == 1 || n == 2) {
            return 1;
        }
        for (int i = 3; i <= n; i++) {
            dp[i] = (dp[i - 1] + dp[i - 2]) % 1000000007;
        }
        return dp[n];
    }
};
```