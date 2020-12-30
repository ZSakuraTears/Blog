---
title: '整数反转(数组)'
date: 2020-12-06 17:16:41
tags: [算法,LeetCode,数组]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(7).jpg.webp
isTop: false
---
### 题目
给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。<br><br>
<!-- more -->
示例 1:

输入: 123
输出: 321<br><br>

 示例 2:

输入: -123
输出: -321<br><br>

示例 3:

输入: 120
输出: 21<br><br>

注意:<br><br>

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为 [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 题解
多注意爆int的地方，多wa几发就过了~~手动狗头~~
```C++
class Solution {
public:
    int reverse(int x) {
        int j = 0, m = 0, num = 0, jud = 0;
        char str[1000];
        int i = 0;
        if (x < 0)
        {
            if (x <= -pow(2, 31)) // 负数正好没爆int，转正可能就会正好爆
                return 0;
            x = -x;
            jud = 1;
        }
        while (x > 0)
        {
            str[i++] = x % 10 + 48;
            x /= 10;
        }
        str[i] = '\0';
        if (str[0] == '0')
        {
            m = 1;
        }
        for (int i = m; str[i] != '\0'; i++)
        {
            j++;
        }
        j--;
        for (int i = m; str[i] != '\0'; i++)
        {
            if ((str[i] - 48) * pow(10, j) > pow(2, 31) - 1 || (str[i] - 48) * pow(10, j) < -pow(2, 31)) { //可能爆int的地方
                return 0;
            }
            if (num + (str[i] - 48) * pow(10, j) > pow(2, 31) - 1 || num + (str[i] - 48) * pow(10, j) < -pow(2, 31)) {  //可能爆int的地方
                return 0;
            }
            num += (str[i] - 48) * pow(10, j);
            j--;
        }
        if (jud != 0)
        {
            num = -num;
        }
        return num;
    }
};
```