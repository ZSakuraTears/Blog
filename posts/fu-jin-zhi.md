---
title: '负进制'
date: 2020-10-23 14:55:30
tags: [算法]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(8).jpg.webp
isTop: false
---
### 题目描述

![洛谷](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/chrome_kZgFEYVhht.png)

### 输入格式
输入的每行有两个输入数据。
第一个是十进制数 n。 第二个是负进制数的基数 −R。

### 输出格式
输出此负进制数及其基数，若此基数超过 10，则参照 16 进制的方式处理。

### 输入输出样例
输入 3000 -2
输出 30000=11011010101110000(base-2)
输入 -20000 -2
输出 -20000=1111011000100000(base-2)
输入 28800 -16
输出 28800=19180(base-16)
输入 -25000 -16
输出 -25000=7FB8(base-16)

### 说明
【数据范围】
对于 100% 的数据,−20≤R≤−2,∣n∣≤37336。

NOIp2000提高组第一题


### 题解：
正常情况下-7 % -2 商4 余1
但是C语言（或者说所有语言）这里是商3 余-1
这就很明显了，只需要把商+1，被除数+1就和正常计算情况一样了



#### 代码为：

```C/C++
#include <stdio.h>

void zh(int a, int b)
{
    if (a == 0) {
        return;
    }
    int m = a % b;
    if (m < 0) {
        m -= b;
        a += b;
    }
    if (m > 9) {
        m = 'A' + m - 10;
    }
    else
        m += '0';
    zh(a / b, b);
    printf("%c", m);
}

int main()
{
    int a, b;
    scanf("%d%d", &a, &b);
    printf("%d=", a);
    zh(a, b);
    printf("(base%d)", b);
    return 0;
}
```