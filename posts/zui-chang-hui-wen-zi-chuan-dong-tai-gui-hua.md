---
title: '最长回文子串(动态规划)'
date: 2020-12-04 19:47:51
tags: [算法,LeetCode,动态规划]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(3).jpg.webp
isTop: false
---
### 题目
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。<br><br>
<!-- more -->
示例 1：
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。<br><br>

示例 2：
输入: "cbbd"
输出: "bb"<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-palindromic-substring
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>


### 题解
#### 暴力求解
把每个长度大于二的子串都进行验证，然后取最大，时间复杂度O(n3)，然后就愉快的超时0.0
```C++
class Solution {
public:
    bool vali(string s, int i, int j)
    {
        while (i <= j) {
            if (s[i] != s[j])
                return false;
            i++;
            j--;
        }
        return true;
    }
    string longestPalindrome(string s) {
        int size = s.size();
        if (size < 2)
            return s;
        int max = 1;
        string str = s.substr(0, 1);
        for (int i = 0; i < size - 1; i++) {
            for (int j = i + 1; j < size; j++) {
                if (j - i + 1 > max && vali(s, i, j)) {
                    max = j - i + 1;
                    str = s.substr(i, max);
                }
            }
        }
        return str;
    }
};
```

#### 动态规划
动态规划关键步骤状态转移：
一个回文去掉两头以后，剩下的部分依然是回文；
如果一个字符串的头尾两个字符都不相等，那么这个字符串一定不是回文串；
如果一个字符串的头尾两个字符相等，才有必要继续判断下去。
如果里面的子串是回文，整体就是回文串；
如果里面的子串不是回文串，整体就不是回文串。<br><br>

定义dp[i][j]表示s[i....j]是否为回文串(左闭右闭)，根据“如果里面的子串判断是否回文”，可以得到转移方程：dp[i][j] = (s[i] == s[j]) && dp[i + 1][j - 1] == true<br><br>

然后考虑一下边界问题：<br><br>
s[i + 1......j - 1]，成立的条件为长度小于2，即j - 1 - (i + 1) < 2，即j - i < 3.
j - i < 3 等价于 j - i + 1 < 4，即当子串 s[i..j] 的长度等于 2 或者等于 3 的时候，其实只需要判断一下头尾两个字符是否相等就可以直接下结论了。<br><br>

如果子串 s[i + 1..j - 1] 只有 1 个字符，即去掉两头，剩下中间部分只有 1 个字符，显然是回文；
如果子串 s[i + 1..j - 1] 为空串，那么子串 s[i, j] 一定是回文子串。<br><br>

因此，在 s[i] == s[j] 成立和 j - i < 3 的前提下，直接可以下结论，dp[i][j] = true，否则才执行状态转移。<br><br>

```C++
class Solution {
public:
    string longestPalindrome(string s) {
        int len = s.size();
        if (len < 2)
            return s;
        int begin = 0;
        int max = 1; //记录回文子串开始位置和长度
        bool dp[len][len];
        for (int i = 0; i < len; i++) {
            dp[i][i] = true; //初始化，单个字符一定是回文串，因此把对角线先初始化为 true，即 dp[i][i] = true 
        }
        for (int j = 1; j < len; j++) {
            for (int i = 0; i < j; i++) {
                if (s[i] != s[j]) {
                    dp[i][j] = false;
                }
                else {
                    if (j - i < 3) {
                        dp[i][j] = true;
                    }
                    else {
                        dp[i][j] = dp[i + 1][j - 1];
                    }
                }
                if (dp[i][j] && j - i + 1 > max) {
                    begin = i;
                    max = j - i + 1;
                }
            }
        }
        string str = "";
        for (int i = begin; i < begin + max; i++) {
            str += s[i];
        }
        return str;
    }
};
```

思路参考：liweiwei1419