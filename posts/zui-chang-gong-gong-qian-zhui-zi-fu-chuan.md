---
title: '最长公共前缀(字符串)'
date: 2020-12-18 17:02:23
tags: [算法,字符串,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(7).jpg.webp
isTop: false
---
### 题目
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。
<!-- more -->
示例 1:

输入: ["flower","flow","flight"]
输出: "fl"
示例 2:

输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
说明:

所有输入只包含小写字母 a-z 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-common-prefix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
直接每个字符串从头开始元素比较，不一样直接return即可A
```C++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string str = "";
        if (strs.size() == 0) {
            return str;
        }
        char ch;
        int i, j, min = INT_MAX;
        for (int m = 0; m < strs.size(); m++) {
            if (strs[m].size() < min) {
                min = strs[m].size();
            }
        }
        for (i = 0; i < min; i++) {
            ch = strs[0][i];
            for (j = 0; j < strs.size(); j++) {
                if (strs[j][i] != ch) {
                    return str;
                }
            }
            str += ch;
        }
        return str;
    }
};
```