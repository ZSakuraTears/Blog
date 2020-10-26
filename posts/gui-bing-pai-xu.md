---
title: '归并排序'
date: 2020-10-23 14:57:28
tags: [算法,排序]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(6).jpg.webp
isTop: false
---
归并排序将两个有序的排列归并为一个有序的排列。

归并算法都基于归并这个简单的操作，即将两个有序的数组归并成一个更大的有序数组。很快人们就根据这个操作发明了一种简单的递归排序算法：归并排序。要将一个数组排序，可以先（递归地）将它分成两半分别排序，然后将结果归并起来：你将会看到，归并排序最
吸引人的性质是它能够保证将任意长度为，的数组排序所需时间和，成正比；它的主要缺点则是它所需的额外空间。简单的归并排序如图所示。

![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/FoxitPhantom_6xnNTxUAow.png)

#### 原地归并

先创建一个数组aux将a的元素全部赋给aux。然后开始将两个有序的数组归并成一个有序的数组。
将a[lo, mid]和a[mid + 1, hi]两个有序数组归并为一个有序数组
![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/FoxitPhantom_1FWin67kuQ.png)

```C/C++
void merge(int a[], int lo, int mid, int hi)
{
    int i, j;
    i = lo;
    j = mid + 1;
    int aux[hi + 1];
    for (int k = lo; k <= hi; k++)
    {
        aux[k] = a[k];
    }
    for (int k = lo; k <= hi; k++)
    {
        if (i > mid)
        {
            a[k] = aux[j++];
        }
        else if (j > hi)
        {
            a[k] = aux[i++];
        }
        else if (aux[j] < aux[i])
        {
            a[k] = aux[j++];
        }
        else
        {
            a[k] = aux[i++];
        }
    }
}
```
当左边（mid为中界）元素已经全部赋值到a中时，则不需要再考虑左边元素，直接把右边剩余元素全部赋值给a即可  if(i > mid)
当右边（mid为中界）元素已经全部赋值到a中时，则不需要再考虑右边元素，直接把左边剩余元素全部赋值给a即可  if(j > hi)
如果右边当前元素小于左边当前元素则将右边当前元素赋给a,(aux[j] < aux[i])
右边当前元素大于等于左边当前元素，最后一个else

#### 自上向下

自顶向下归并将一个数组先中间拆分，再把拆分的数组拆分，直到只有一个元素的数组，然后将每两个数组就行归并。最后归并为一个有序数组。
![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/FoxitPhantom_pNM5lWqMZA.png)
![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/FoxitPhantom_VlHXNLFh2k.png)

```C/C++
void gbsort(int a[], int lo, int hi)
{
    if (hi <= lo)
    {
        return;
    }
    int mid;
    mid = lo + (hi - lo) / 2;
    gbsort(a, lo, mid);
    gbsort(a, mid + 1, hi);
    merge(a, lo, mid, hi);
}
```
#### 自底向上

自底向上归并第一次每两个元素的数组归并，然后每四个，八个......归并，最终归并成一个有序数组
![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/FoxitPhantom_3ixOLZEZqD.png)

```c/c++
void gbsort(int a[], int lo, int hi)
{
    int n = hi + 1; //n为数组长度
    for (int i = 1; i < n; i += i)//每次循环完了归并前一次翻倍的数组元素个数
    {
        for (int j = 0; j < n - i; j += i * 2)
        {
            if (j + i * 2 - 1 < hi)
            {
                merge(a, j, j + i - 1, j + i * 2 - 1);
            }
            else {
                merge(a, j, j + i - 1, hi);
            }
        }
    }
}
```