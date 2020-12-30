---
title: 'C语言实现各种进制之间转换'
date: 2020-12-20 19:55:47
tags: [C/C++]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/ycL3yPmxeH.jpg
isTop: false
---
```C
#include <Windows.h>
#include <math.h>
#include <stdio.h>
#include <string.h>

#define N 50

//进制转换

char *Ten_MoreThanTen(int, int); //10进制数转换成10以上进制数的函数

int MoreThanTen_Ten(int, char[]); //10以上进制数转换成10进制数的函数

int Ten_LessThanTen(int, int); //10进制数转换成10以内进制数的函数

int LessThanTen_Ten(int, int); //10以内进制数转换成10进制数的函数

char array[N] = "\0"; //全局变量，用于存储转换后并且倒置了的数据

int LessThanTen_Ten(int before, int num) //10以内转换10，参数brfore为初始进制,num为初始数值

{

    double result = 0.0; //转换成10进制后的结果

    int i = 0;

    for (i = 0; num != 0; i++) //利用for循环实现按权展开相加

    {

        result += pow(before, i) * (num % 10);

        num /= 10;
    }

    return (int)result; //返回值为转换后的结果
}

int Ten_LessThanTen(int after, int num) //10转换10以内，参数after为转换后的进制，num为10进制数值

{

    double result = 0.0; //double类型因为pow函数的返回值为double类型

    int i = 0;

    for (i = 0; num != 0; i++) //利用for循环实现连续取余

    {

        result += (num % after) * pow(10, i);

        num /= after;
    }

    return (int)result;
}

int MoreThanTen_Ten(int before, char num[]) //10以上转换10

{

    int i = 0;

    double result = 0.0;

    int length = strlen(num);

    for (i = length - 1; i >= 0; i--)

    {

        //利用ASCALL码将所有元素转换成对应的整型

        if ('A' <= num[i] && num[i] <= 'Z')

            result += pow(before, length - i - 1) * (num[i] - 55);

        else if ('a' <= num[i] && num[i] <= 'z')

            result += pow(before, length - i - 1) * (num[i] - 87);

        else if ('0' <= num[i] && num[i] <= '9')

            result += pow(before, length - i - 1) * (num[i] - 48);
    }

    return (int)result;
}

char *Ten_MoreThanTen(int after, int num) //10转换10以上

{

    int i = 0;

    int j = 0;

    int tmp = 0; //存储每次余数的中间变量

    char tmp_array[N] = "\0"; //转换后未倒置的数组

    for (i = 0; num > 0; i++)

    {

        tmp = num % after;

        if (tmp < 10) //对大于等于10的余数进行字母转换

            tmp_array[i] = tmp + '0';

        else

            tmp_array[i] = tmp + 'A' - 10;

        num /= after;
    }

    for (j = 0; i > 0; i--, j++) //倒置

    {

        array[j] = tmp_array[i - 1];

        array[j + 1] = '\0';
    }

    return array; //输出转换后存储数据的字符串地址
}

int main()

{

    int before = 0; //转换前的进制数

    int after = 0; //转换后的进制数

    int num1 = 0; //要转换的十进制以内的数

    char array_num1[N] = "\0"; //要转换的十进制以上的数

    int num2 = 0; //转换之后的数

    char *str_num2; //转换之后的数的地址

    int tmp_num1 = 0; //判断输入是否合法时代替num1的中间变量

    int i = 0;

    int m = 0; //计数器

    while (1) //整个while语句用于录入以及判断输入是否合法

    {

        printf("初始进制：");

        scanf("%d", &before);

        printf("目标进制：");

        scanf("%d", &after);

        printf("初始数值：");

        if (before > 10) //通过对初始进制判断，决定

            scanf("%s", array_num1);

        else

            scanf("%d", &num1);

        for (i = 0, tmp_num1 = num1; tmp_num1 != 0; i++)

        {

            if ((tmp_num1 % 10) <= before && tmp_num1 % 10 >= 0 && tmp_num1 % 10 <= 9)

                m++;

            tmp_num1 /= 10;
        }

        if (m == i) //判断输入的数据每一位是否都小于等于进制数

            break;

        else

        {

            m = 0; //对计数器m重新初始化

            fflush(stdin); //清空缓存区

            printf("输入有误！请重新输入：\n");
        }
    }

    //将进制转换的四种情况分别表示

    if (before <= 10 && after <= 10)

    {

        num2 = Ten_LessThanTen(after, LessThanTen_Ten(before, num1));

        printf("\n%d进制的%d对应的%d进制数为：%d\n", before, num1, after, num2);
    }

    else if (before > 10 && after <= 10)

    {

        num2 = Ten_LessThanTen(after, MoreThanTen_Ten(before, array_num1));

        printf("\n%d进制的%s对应的%d进制数为：%d\n", before, array_num1, after, num2);
    }

    else if (before <= 10 && after > 10)

    {

        str_num2 = Ten_MoreThanTen(after, LessThanTen_Ten(before, num1));

        printf("\n%d进制的%d对应的%d进制数为：%s\n", before, num1, after, str_num2);
    }

    else if (before > 10 && after > 10)

    {

        str_num2 = Ten_MoreThanTen(after, MoreThanTen_Ten(before, array_num1));

        printf("\n%d进制的%s对应的%d进制数为：%s\n", before, array_num1, after, str_num2);
    }

    system("pause");

    return 0;
}
```