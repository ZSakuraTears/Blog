---
title: '堆排序(排序)'
date: 2020-12-25 18:02:22
tags: [排序,数据结构]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/Dl0g4BB4Fp.jpg
isTop: false
---
### 定义
**堆排序**：是指利用堆这种数据结构所设计的一种排序算法。堆是一个近似完全二叉树的结构，并同时满足堆的性质：即子节点的键值或索引总是小于（或者大于）它的父节点。

### 概述
若以升序排序说明，把数组转换成最大堆(Max-Heap Heap)，这是一种满足最大堆性质(Max-Heap Property)的二叉树：对于除了根之外的每个节点i, A[parent(i)] ≥ A[i]。
重复从最大堆取出数值最大的结点(把根结点和最后一个结点交换，把交换后的最后一个结点移出堆)，并让残余的堆维持最大堆性质。

### 堆节点的访问
通常堆是通过一维数组来实现的。在数组起始位置为0的情形中：

父节点i的左子节点在位置(2i + 1);
父节点i的右子节点在位置(2i + 2));
子节点i的父节点在位置(i - 1) / 2;

### 操作
在堆的数据结构中，堆中的最大值总是位于根节点（在优先队列中使用堆的话堆中的最小值位于根节点）。堆中定义以下几种操作：

 - 最大堆调整（Max Heapify）：将堆的末端子节点作调整，使得子节点永远小于父节点
 - 创建最大堆（Build Max Heap）：将堆中的所有数据重新排序
 - 堆排序（HeapSort）：移除位在第一个数据的根节点，并做最大堆调整的递归运算

### 代码实现
```C++
#include <malloc.h>
#include <stdio.h>
#include <stdlib.h>

void swap(int *a, int *b)
{
    int temp = *b;
    *b = *a;
    *a = temp;
}

void max_heapify(int arr[], int start, int end)
{
    // 建立父节点指标和子节点指标
    int dad = start;
    int son = dad * 2 + 1;
    while (son <= end)
    {                                                  // 若子节点指标在范围内才做比较
        if (son + 1 <= end && arr[son] < arr[son + 1]) // 先比较两个子节点大小，选择最大的
            son++;
        if (arr[dad] > arr[son]) //如果父节点大于子节点代表调整完毕，直接跳出函数
            return;
        else
        { // 否则交换父子内容再继续子节点和孙节点比较
            swap(&arr[dad], &arr[son]);
            dad = son;
            son = dad * 2 + 1;
        }
    }
}

void heap_sort(int arr[], int len)
{
    int i;
    // 初始化，i从最后一个父节点开始调整
    for (i = len / 2 - 1; i >= 0; i--)
        max_heapify(arr, i, len - 1);
    // 先将第一个元素和已排好元素前一位做交换，再重新调整，直到排序完毕
    for (i = len - 1; i > 0; i--)
    {
        swap(&arr[0], &arr[i]);
        max_heapify(arr, 0, i - 1);
    }
}

int main()
{
    // int arr[] = {9, 10, 5, 11, 12, 7};
    // int len = (int)sizeof(arr) / sizeof(*arr);

    int len;
    printf("输入数组长度");
    scanf("%d", &len);
    int *arr = (int *)malloc(sizeof(int) * len);
    printf("输入数组：");
    for (int i = 0; i < len; i++)
    {
        scanf("%d", &arr[i]);
    }
    heap_sort(arr, len);
    int i;
    for (i = 0; i < len; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

(来自：维基百科)