---
title: 'C语言实现链表基本操作（交换第i个和第j个节点）'
date: 2020-10-23 14:39:58
tags: []
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(3).jpg.webp
isTop: false
---
## C语言实现链表基本操作（交换第i个和第j个节点） 

### 当i或者j为1时，需要让链表的表头指向j。
![开始时](https://img-blog.csdnimg.cn/20200611081240188.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_8,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611081335308.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_8,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061108140129.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_8,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611081415319.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_8,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611081427878.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_8,color_FFFFFF,t_70)
代码为
```c
/*i和j为1时情况比较特殊，需要让表头重新指向交换后的那个节点*/
    if (i == 1) { 
        t1 = *L;
        for (m = 1; temp->Next != NULL; m++, temp = temp->Next) {
            if (m + 1 == j) {
                *L = temp->Next;
                t2 = temp->Next->Next;
                temp->Next->Next = t1->Next;
                t1->Next = t2;
                temp->Next = t1;
            }
        }
    }
```
### 当i和j都不为1时。
节点相邻与不相邻也是不一样的。
不相邻的情况下就是让i前面的节点指向j，然后让j前面的节点指向i。如果两个节点相邻（假设i < j）j前面的节点就是i，j前面的节点指向i就是指向了自己，所以要分开写。
不相邻节点时：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611083309796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611083331554.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611083418720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611083435638.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
代码为：
```c
if ((i - j) != 1 && (j- i) != 1) {//非相邻结点之间交换
            for (m = 1; temp->Next != NULL; m++, temp = temp->Next) {
                if (m + 1 == i) {
                    t1 = temp;
                }
                if (m + 1 == j) {
                    t2 = temp;
                }
            }
            t5 = t1->Next->Next;
            t3 = t1->Next;
            t4 = t2->Next;
            t1->Next = t4;
            t2->Next = t3;
            t3->Next = t4->Next;
            t4->Next = t5;
        }
```
### 最后一种情况，两个节点相邻：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611084227643.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611084240634.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611084255116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611084305639.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L20wXzQ2MDg5ODUw,size_16,color_FFFFFF,t_70)
代码为：
```c
for (m = 1; temp != NULL; m++, temp = temp->Next) {
                if (m + 1 == i) {
                    t1 = temp;
                }
                if (m == j) {
                    t2 = temp;
                }
            }
            temp = t2->Next;
            t3 = t1->Next;
            t1->Next = t2;
            t3->Next = temp;
            t2->Next = t3;
        }
```
全部代码：
```c
#include <stdio.h>
#include <malloc.h>

typedef struct node
{
    int Score;
    struct node * Next;
}Node, * List;

void Insert(List *L, Node e)
{
    List temp = *L;
    List n = (List)malloc(sizeof(Node));
    n->Score = e.Score;
    if (temp == NULL) {
        *L = n;
    }
    else {
        while (temp->Next != NULL) {
            temp = temp->Next;
        }
        temp->Next = n;
    }
    n->Next = NULL;
}

void Swap(List * L, int i, int j)
{
    List temp = *L;
    List t1;
    List t2;
    List t3;
    List t4;
    List t5;
    int m;
    /*i和j为1时情况比较特殊，需要让表头重新指向交换后的那个节点*/
    if (i == 1) { 
        t1 = *L;
        for (m = 1; temp->Next != NULL; m++, temp = temp->Next) {
            if (m + 1 == j) {
                *L = temp->Next;
                t2 = temp->Next->Next;
                temp->Next->Next = t1->Next;
                t1->Next = t2;
                temp->Next = t1;
            }
        }
    }
    if (j == 1) {
        t1 = *L;
        for (m = 1; temp->Next != NULL; m++, temp = temp->Next) {
            if (m + 1 == i) {
                *L = temp->Next;
                t2 = temp->Next->Next;
                temp->Next->Next = t1->Next;
                t1->Next = t2;
                temp->Next = t1;
            }
        }
    }
    /*相邻节点之间交换和非相邻结点之间交换不一样*/
    else {
        if ((i - j) != 1 && (j- i) != 1) {//非相邻结点之间交换
            for (m = 1; temp->Next != NULL; m++, temp = temp->Next) {
                if (m + 1 == i) {
                    t1 = temp;
                }
                if (m + 1 == j) {
                    t2 = temp;
                }
            }
            t5 = t1->Next->Next;
            t3 = t1->Next;
            t4 = t2->Next;
            t1->Next = t4;
            t2->Next = t3;
            t3->Next = t4->Next;
            t4->Next = t5;
        }
        else if (i < j) {//相邻节点之间交换
            for (m = 1; temp != NULL; m++, temp = temp->Next) {
                if (m + 1 == i) {
                    t1 = temp;
                }
                if (m == j) {
                    t2 = temp;
                }
            }
            temp = t2->Next;
            t3 = t1->Next;
            t1->Next = t2;
            t3->Next = temp;
            t2->Next = t3;
        }
        else if (i > j) {
            for (m = 1; temp != NULL; m++, temp = temp->Next) {
                if (m + 1 == j) {
                    t1 = temp;
                }
                if (m == i) {
                    t2 = temp;
                }
            }
            temp = t2->Next;
            t3 = t1->Next;
            t1->Next = t2;
            t3->Next = temp;
            t2->Next = t3;
        }
    }
}

void printflist(List list) 
{
    List temp;
    for (temp = list; temp != NULL; temp = temp->Next) {
        printf("%d\n", temp->Score);
    }
}

void freelist(List *list)
{
    List temp = *list, del;
    while (temp != NULL) {
        del = temp;
        temp = temp->Next;
        free(del);
    }
}

int main()
{
    List list = NULL;
    Node n1, n2, n3, n4, e;//定义5个节点
    e.Score = 5;
    n1.Score = 1;
    n2.Score = 2;
    n3.Score = 3;
    n4.Score = 4;
    Insert(&list, n1);
    Insert(&list, n2);
    Insert(&list, n3);
    Insert(&list, n4);
    Insert(&list, e);
    // dellist(&list, 8);
    Swap(&list, 5, 4);
    printflist(list);
    freelist(&list);
    return 0;
}


```