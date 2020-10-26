---
title: 'C语言链表基本操作（头插法及其逆置）'
date: 2020-10-23 14:32:17
tags: []
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(5).jpg.webp
isTop: false
---
```C/C++
#include <stdio.h>
#include <malloc.h>

typedef struct Node
{
    char data;
	struct Node *next;
}SN;

SN * create(int n)
{
	int i;
	SN *h,*p;
    h = NULL;
    for(i = 0; i<n; i++)
	{
		p=(SN*)malloc(sizeof(SN));
		printf("请输入第%d个字符：",i+1);
		p->data = getchar();
		fflush(stdin);
		p->next = h;
		h=p;
	}
	return h;
}

SN * def(SN * h)
{ 
    SN * n1, *n2;
	n1 = h;
	n2 = NULL;
	while(n1 != NULL)
	{
		SN *temp;
		temp = n1;
		n1 = n1->next;
		temp->next = n2;
		n2 = temp;
	}
	h = n2;
	return h;
}
void visit(SN * h)
{ 
	while(h != NULL)
	{
		printf("%c", h->data);
		h = h->next;
	}
	printf("\n");
}

void freelist(SN *h)
{
    SN *temp = h;
	SN *del;
	while (temp != NULL) {
        del = temp;
        temp = temp->next;
        free(del);
    }
}

int main() 
{
	int n;
	SN *h;
	printf("请输入字符个数：\n");
	scanf("%d", &n);
	fflush(stdin);
	h = create(n);
	printf("链表创建成功，对其遍历\n");
    visit(h);
	printf("链表逆置成功，对其遍历\n");
	h = def(h);
	visit(h);
	freelist(h);
	return 0;
}
```