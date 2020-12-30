---
title: '找不同(位运算)(哈希表)'
date: 2020-12-18 17:38:22
tags: [算法,LeetCode,位运算,哈希表]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/Dl0g4BB4Fp.jpg
isTop: false
---
### 题目
给定两个字符串 s 和 t，它们只包含小写字母。
字符串 t 由字符串 s 随机重排，然后在随机位置添加一个字母。
请找出在 t 中被添加的字母。
<!-- more -->
 

示例 1：
输入：s = "abcd", t = "abcde"
输出："e"
解释：'e' 是那个被添加的字母。

示例 2：
输入：s = "", t = "y"
输出："y"

示例 3：
输入：s = "a", t = "aa"
输出："a"

示例 4：
输入：s = "ae", t = "aea"
输出："a"
 
提示：

0 <= s.length <= 1000
t.length == s.length + 1
s 和 t 只包含小写字母

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-the-difference
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
#### 方法1：位运算
^运算符：0与任何数ch做^运算都是ch
相同字符异或为0

因为t中的字符是s + ch，所以s与t做异或剩下的就是ch
```C++
class Solution {
public:
    char findTheDifference(string s, string t) {
        char res = 0;
        for(char c : s + t) {
            res ^= c;
        }
        return res;
    }
};
```
#### 方法2：哈希表
把s中所有元素存到一个哈希表mpS里，t中所有元素存到一个哈希表mpT里
然后比较两个哈希表每个元素个数，不一样的就是题目所求
```C++
char findTheDifference(string s, string t) {
        unordered_map<char, int> mpS;
        unordered_map<char, int> mpT;
        char ch;
        for (auto ch : s) {
            mpS[ch]++;
        }
        for (auto ch : t) {
            mpT[ch]++;
        }

        for (ch = 'a'; ch <= 'z'; ch++) {
            if (mpS[ch] != mpT[ch]) {
                return ch;
            }
        }
        return ch;
    }
    ```