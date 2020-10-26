---
title: '快速排序'
date: 2020-10-23 14:59:36
tags: [算法,排序]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(3).jpg.webp
isTop: false
---
快速排序的特点是他是原地排序（只需要一个很小的辅助栈），且长度为N的数组时间复杂度为NlgN。
快速排序是一种分治的算法，他将一个数组分成两个数组，将两部分独立排序，在快排中切分的位置取决于数组的内容。
取首元素为切分元素，比切分元素小的放到左边，比切分元素大的放到右边，再把两个数组切分，最后有序
![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/QQ%E5%9B%BE%E7%89%8720201015164728.jpg)
```C/C++
void qsort(int a[], int lo, int hi)
{
    if (lo >= hi)
        return;
    int i, j, m, temp, mid;
    m = a[lo]; //切分元素
    i = lo; //下面循环时i和j就会先自增/自减1再判断，所以i为头元素，j为尾元素 - 1
    j = hi + 1;
    while (true)
    {
        while (a[++i] < m)
        {
            if (i == hi)//直到循环到右边界也没有找到比切分元素大的元素
                break;
        }
        while (a[--j] > m)
        {
            if (j == lo)//直到循环到左边界也没有找到比切分元素小的元素
                break;
        }
        if (i >= j)//当i的位置在j的右边，a[i] > a[j],不可以交换
            break;
        int temp = a[i];
        a[i] = a[j];
        a[j] = temp;
    }
    temp = a[lo];
    a[lo] = a[j];
    a[j] = temp;
    mid = j;
    qsort(a, lo, mid - 1);
    qsort(a, mid + 1, hi);
}
```