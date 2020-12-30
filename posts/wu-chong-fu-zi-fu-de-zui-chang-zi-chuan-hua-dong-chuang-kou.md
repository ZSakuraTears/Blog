---
title: '无重复字符的最长子串(滑动窗口)'
date: 2020-12-13 17:21:43
tags: [算法,LeetCode,滑动窗口]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/54lqq0%20(1).jpg
isTop: false
---
### 题目
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。
<!-- more -->
 

示例 1:

输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。<br><br>
示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。<br><br>
示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。<br><br>
示例 4:

输入: s = ""
输出: 0<br><br>
 

提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
定义p为子串的头，j为尾部，p到j为一个窗口，如果新的元素i和窗口里的元素相同，则把p移动到i的后面。记录每一个窗口的长度，最后取最大
```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s)
    {
        if (s.size() == 0)
        {
            return 0;
        }
        int i, j, max, n, p, jud = 0;
        i = 0;
        p = i;
        j = i + 1;
        max = 1;
        n = 1;
        for (; j < s.size(); j++)
        {
            jud = 0;
            for (p = i; p < j; p++)
            {
                if (s[p] == s[j])
                {
                    i = p + 1;
                    if (i == j)
                    {
                        n = 1;
                    }
                    else if (s[i] == s[j])
                    {
                        n = j - i;
                    }
                    else
                    {
                        n = j - i + 1;
                    }
                    jud = 1;
                    break;
                }
            }
            if (jud == 1)
            {
                continue;
            }
            n++;
            if (n > max)
                max = n;
        }
        return max;
    }
};
```