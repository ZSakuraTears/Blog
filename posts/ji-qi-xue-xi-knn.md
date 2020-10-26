---
title: '机器学习-knn'
date: 2020-10-04 14:58:31
tags: [机器学习]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(9).jpg.webp
isTop: true
---
```python
import math
import numpy#导入两个库

def knn(c):#定义knn函数
    k_a = 0
    k_b = 0
    distance_a = []#定义a和c的距离列表
    distance_b = []#定义b和c的距离列表
    distance = []#所有数据距离列表
    for i in range(0, len(a)):#a的每个数据和c的每个数据的距离
        distance_a.append(math.sqrt(numpy.square(a[i][0] - c[0]) + numpy.square(a[i][1] - c[1])))
    for i in range(0, len(b)):#b的每个数据和c的每个数据的距离
        distance_b.append(math.sqrt(numpy.square(b[i][0] - c[0]) + numpy.square(b[i][1] - c[1])))
    distance = distance_a + distance_b
    distance.sort()#排序距离
    k = int(len(distance) / 2) + 1#取k的值
    for i in range(k):
        if distance_a.count(distance[i]) != 0:#判断该距离是否是a和c的距离
            k_a = k_a + 1
        if distance_b.count(distance[i]) != 0:#判断该距离是否是b和c的距离
            k_b = k_b + 1
    if k_a > k_b:#判断c的数据和哪个类别接近
        print("你属于肥胖身材")
    else:
        print("你属于标准身材")


a = [[150, 60], [152, 65], [154, 68], [156, 70], [158, 72]]#类别a
b = [[150, 49.5], [152, 50.8], [154, 52.2], [156, 53.5], [158, 54.9]]#类别b
c = []  #判断类别c
print("输入身高体重")
for i in range(2):#输入c
    num = int(input())
    c.append(num)
knn(c)#调用函数knn

```