---
title: 'LeetCode 387. 字符串中的第一个唯一字符(哈希表)'
date: 2020-12-23 19:54:29
tags: [算法,LeetCode,哈希表]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/gridea-zhu-ti-fog-geng-xin-ri-zhi.jpeg
isTop: false
---
### 题目
给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。
<!-- more -->
示例：

s = "leetcode"
返回 0

s = "loveleetcode"
返回 2
 

提示：你可以假定该字符串只包含小写字母。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/first-unique-character-in-a-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
#### 方法1：哈希表
```C++
class Solution {
public:
    int firstUniqChar(string s) {
        if (s.size() <= 0) {
            return -1;
        }
        map<int, int> smap;
        for (char ch : s) {
            smap[ch]++;
        }
        for (int i = 0; i < s.size(); i++) {
            if (smap[s[i]] == 1) {
                return i;
            }
        }
        return -1;
    }
};
```
#### 方法2：数组
```C++
class Solution {
public:
    int firstUniqChar(string s) {
        int map[26] = {0};
        for (int i = 0; i < s.size(); i++) {
            map[s[i] - 'a']++;
        }
        for (int i = 0; i < s.size(); i++) {
            if (map[s[i] - 'a'] == 1) {
                return i;
            }
        }
        return -1;
    }
};
```