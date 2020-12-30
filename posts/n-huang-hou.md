---
title: 'N皇后(回溯)'
date: 2020-11-06 08:56:46
tags: [算法,LeetCode,回溯]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(9).jpg.webp
isTop: false
---
n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。
<!-- more -->

![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/8-queens.png)<br><br>

上图为 8 皇后问题的一种解法。<br><br>

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。<br><br>

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。<br><br>

 

示例：<br><br>

输入：4
输出：[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],<br><br>

 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。<br><br>
 

提示：<br><br>

皇后彼此不能相互攻击，也就是说：任何两个皇后都不能处于同一条横行、纵行或斜线上。<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-queens<br><br>

经典回溯+递归问题，当发现这种情况不行时就回溯到之前的点。<br><br>


代码：
```C++
class Solution {
public:
    int col[12] = {};//将合适的皇后行数放入数组中
    vector<vector<string>> arr;
    vector<string> brr;
    char crr[100][100];
    int cnumber = 0;
    int num, number = 0, jud = 0, tot = 0;
    bool check(int c, int r)
    {
        int i = 0;
        for (i = 0; i < r; i++)
        {
            if (col[i] == c || (abs(col[i] - c) == abs(i - r)))
                return false;
        }
        return true;
    }

    void DFS(int r)
    {
        if (r == num)
        {
            string str = "";
            brr.clear();
            for (int j = 0; j < num; j++)
            {
                str = "";
                
                for (int i = 0; i < num; i++)
                {
                    if (crr[j][i] == 'Q')
                        str += "Q";
                    else
                        str += ".";
                }
                brr.push_back(str);
            }
            arr.push_back(brr);
            return;
        }
        for (int c = 0; c < num; c++)
        {
            if (check(c, r) == true)
            {
                col[r] = c;
                int i = 0;
                while (i < num)
                {
                    if (i == c)
                    {
                        crr[r][i] = 'Q';
                    }
                    else
                        crr[r][i] = '.';
                    i++;
                }
                DFS(r + 1);
            }
        }
    }

    vector<vector<string>> solveNQueens(int n)
    {
        num = n;
        DFS(0);
        return arr;
    }
};
```
