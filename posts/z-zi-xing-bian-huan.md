---
title: 'Z 字形变换(字符串)'
date: 2020-12-05 20:51:16
tags: [LeetCode,算法,字符串]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(1).jpg.webp
isTop: false
---
### 题目
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。<br>
<!-- more -->
比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：<br>

L   C   I   R
E T O E S I I G
E   D   H   N
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。<br>

请你实现这个将字符串进行指定行数变换的函数：<br>

string convert(string s, int numRows);<br>

示例 1:
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"<br>

示例 2:
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:<br>

L     D     R
E   O E   I I
E C   I H   N
T     S     G<br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/zigzag-conversion
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br>

### 思路
#### 代码1.
纯暴力写出来了，贴个代码算了0.0
```C++
class Solution {
public:
    string convert(string s, int numRows)
    {
        if (numRows == 1)
            return s;
        int num = 0, m = 0, p = 1, j = 0;
        char arr[1000][1000];
        string str;
        for (int i = 0; i < 1000; i++)
        {
            for (int j = 0; j < 1000; j++)
            {
                arr[i][j] = NULL;
            }
        }
        for (int i = 0; num < s.size(); i++)
        {
            for (j = 0; j < numRows && num < s.size(); j++)
            {
                if (i == 0 || i == m + numRows - 1)
                {
                    m = i;
                    for (j = 0; j < numRows && num < s.size(); j++)
                    {
                        arr[j][i] = s[num];
                        num++;
                    }
                    p = 0;
                    continue;
                }
                else
                {
                    if (j != numRows - 1 && arr[j + 1][i - 1] != NULL)
                    {
                        if (i != m + 1 && i != 1)
                        {
                            arr[j][i] = s[num];
                            p = 0;
                            num++;
                            continue;
                        }
                        else
                        {
                            j = numRows - 2;
                            arr[j][i] = s[num];
                            i++;
                            j = -1;
                            num++;
                            continue;
                        }
                    }
                }
            }
        }
        for (int i = 0; i < s.size() && str.size() != s.size(); i++)
        {
            for (int j = 0; j < s.size() && str.size() != s.size(); j++)
            {
                if (arr[i][j] >= 41 && arr[i][j] <= 176)
                {
                    str += arr[i][j];
                }
            }
        }
        return str;
    }
};
```

#### 代码2
1.res[i] += c： 把每个字符 c 填入对应行 s i;
2.i += flag： 更新当前字符 c 对应的行索引；
3.flag = - flag： 在达到 Z 字形转折点时，执行反向<br>

把每一行放到一个字符串数组里面，利用flag就行上下控制。~~比我那菜鸡算法好太多了~~
```C++
class Solution {
public:
    string convert(string s, int numRows)
    {
        if (numRows == 1) {
            return s;
        }
        string str[1000];
        int i = 0, flag = 1, num = 0;
        while (num < s.size())
        {

            str[i] += s[num];
            i += flag;
            if (i >= numRows)
            {
                flag = -flag;
                i += flag;
                i += flag;
            }
            if (i < 0)
            {
                flag = -flag;
                i += flag;
                i += flag;
            }
            num++;
        }
        s = "";
        for (i = 0; i < numRows; i++) {
            s += str[i];
        }
        return s;
    }
};
```


