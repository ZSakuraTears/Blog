---
title: '旋转图像(数组)'
date: 2020-12-19 18:45:03
tags: [算法,数组,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(3).jpg.webp
isTop: false
---
### 题目
给定一个 n × n 的二维矩阵表示一个图像。
将图像顺时针旋转 90 度。
<!-- more -->
说明：

你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。

示例 1:

给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
示例 2:

给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/rotate-image
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
#### 方法1
**题目要求不要用辅助数组，此题解用了辅助数组**
直接用一个辅助数组arr，arr的列是matrix的行，用两个循环即可
```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        vector<vector<int>> arr = matrix;
        for (int i = 0, j = matrix.size() - 1; i < matrix.size(); i++, j--) {
            for (int m = 0; m < matrix[i].size(); m++) {
                arr[m][j] = matrix[i][m];
            }
        }
        matrix = arr;
    }
};
```
#### 方法2
可以先对数组进行从左上到右下对角线为轴进行翻转，再对每一行以中间为轴翻转。即可
```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        if (matrix.size() == 0) {
            return;
        }
        int i, j, m, temp;
        for (i = 0; i < matrix.size() - 1; i++) {
            for (j = i + 1; j < matrix.size(); j++) {
                temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for (i = 0; i < matrix.size(); i++) {
            for (j = matrix[i].size() / 2; j < matrix.size(); j++) {
                temp = matrix[i][j];
                matrix[i][j] = matrix[i][matrix.size() - j - 1];
                matrix[i][matrix.size() - j - 1] = temp;
            }
        }
    }
};
```