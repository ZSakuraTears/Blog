---
title: 'LeetCode 69. x 的平方根(二分)'
date: 2020-12-21 17:32:31
tags: [算法,二分,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(1).jpg.webp
isTop: false
---
### 题目
实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
<!-- more -->
示例 1:

输入: 4
输出: 2
示例 2:

输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sqrtx
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
采用二分法每次找到中间元素与x比较大小，大则在左边查找，小则在右边查找
每次判断一下lo（最左边元素）的平方与lo + 1的平方：
``if (pow(hi, 2) < x && pow(hi + 1, 2) > x)``这就说明x平方根是lo到lo + 1之间的值，所以直接返回lo即可
判断hi同理
```C++
class Solution {
public:
    int res = 0;
    void Sqrt(int lo, int hi, int x) {
        if (pow(lo, 2) == x) {
            res = lo;
            return;
        }
        else if (pow(hi, 2) == x) {
            res = hi;
            return;
        }
        else if (pow(lo, 2) < x && pow(lo + 1, 2) > x) {
            res = lo;
            return;
        }
        else if (pow(hi, 2) < x && pow(hi + 1, 2) > x) {
            res = hi;
            return;
        }
        else if (pow((lo + hi) / 2, 2) == x) {
            res = (lo + hi) / 2;
            return;
        }
        else if (pow((lo + hi) / 2, 2) < x) {
            lo = (lo + hi) / 2;
            Sqrt(lo, hi, x);
        }
        else if (pow((lo + hi) / 2, 2) > x) {
            hi = (lo + hi) / 2;
            Sqrt(lo, hi, x);
        }
    }
    int mySqrt(int x) {
        int lo = 0, hi = x;
        Sqrt(lo, hi, x);
        return res;
    }
};
```