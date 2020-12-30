---
title: '杨辉三角(数组)'
date: 2020-12-07 17:18:43
tags: [算法,LeetCode,数组]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(5).jpg.webp
isTop: false
---
### 题目
给定一个非负整数 numRows，生成杨辉三角的前 numRows 行。<br><br>
<!-- more -->
在杨辉三角中，每个数是它左上方和右上方的数的和。<br><br>

示例:<br><br>

输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/pascals-triangle
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
简单题，直接写就行，leetcode的测试用例也没啥恶心的~~可能是这个题没法恶心了吧~~

```C++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> nums;
        if (numRows == 0) {  //判断0的情况下
            return nums;
        }
        vector<int> num;
        num.push_back(1);
        nums.push_back(num);
        for (int i = 1; i < numRows; i++) {
            vector<int> num;
            num.push_back(1);
            for (int j = 1; j < i; j++) {
                num.push_back(nums[i - 1][j - 1] + nums[i - 1][j]); //每行数组的[j]是上一个数组的[j]位置+[j - 1]位置
            }
            num.push_back(1);
            nums.push_back(num);
        }
        return nums;
    }
};
```