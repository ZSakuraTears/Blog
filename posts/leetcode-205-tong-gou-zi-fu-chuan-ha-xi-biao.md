---
title: 'LeetCode 205. 同构字符串(哈希表)'
date: 2020-12-27 20:13:39
tags: [算法,LeetCode,哈希表]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/54lqq0%20(1).jpg
isTop: false
---
### 题目
给定两个字符串 s 和 t，判断它们是否是同构的。

如果 s 中的字符可以被替换得到 t ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。
<!-- more -->
示例 1:

输入: s = "egg", t = "add"
输出: true
示例 2:

输入: s = "foo", t = "bar"
输出: false
示例 3:

输入: s = "paper", t = "title"
输出: true
说明:
你可以假设 s 和 t 具有相同的长度。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/isomorphic-strings
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
题意为：s中任意一个字符都在t中有唯一对应，t中任意一个字符也都在s中有唯一对应。
所以用两个哈希表一一对应再判断。
```C++
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char, char> map1;
        unordered_map<char, char> map2;
        for (int i = 0; i < s.size(); i++) {
            if (map1.find(s[i]) == map1.end()) { // map1保存s[i] 到 t[j]的映射
                map1[s[i]] = t[i];
            }
            if (map2.find(t[i]) == map2.end()) { // map2保存t[j] 到 s[i]的映射
                map2[t[i]] = s[i];
            }
            // 发现映射 对应不上，立刻返回false
            if (map1[s[i]] != t[i] || map2[t[i]] != s[i]) {
                return false;
            }
        }
        return true;
    }
};
```