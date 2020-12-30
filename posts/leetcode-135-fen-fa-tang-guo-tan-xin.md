---
title: 'LeetCode 135. 分发糖果(贪心)'
date: 2020-12-24 19:14:12
tags: [算法,LeetCode,贪心]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/ycL3yPmxeH.jpg
isTop: false
---
### 题目
老师想给孩子们分发糖果，有 N 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。

你需要按照以下要求，帮助老师给这些孩子分发糖果：

每个孩子至少分配到 1 个糖果。
相邻的孩子中，评分高的孩子必须获得更多的糖果。
那么这样下来，老师至少需要准备多少颗糖果呢？
<!-- more -->
示例 1:

输入: [1,0,2]
输出: 5
解释: 你可以分别给这三个孩子分发 2、1、2 颗糖果。
示例 2:

输入: [1,2,2]
输出: 4
解释: 你可以分别给这三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这已满足上述两个条件。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/candy
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
根据题意得出规则：
A在B左边
左规则：``if(ratings[A] < ratings[B])``则B获得糖比A多
右规则：``if(ratings[A] > ratings[B])``则A获得糖比B多
```markdown
1.先从左到右遍历，将每个人得到糖果数记录到left数组中
    1.将left用1填充（给所有学生一个糖果）
    2.``if (ratings[i] > ratings[i - 1])``则``left[i] = left[i - 1] + 1``
    3.``if (ratings[i] < ratings[i - 1])``不变
2.再从右到左遍历，将每个人得到糖果数记录到right数组中，规则满足右规则
3.最终取left[i]和right[i]中最大值，即可同时满足左规则和右规则
```
```C++
class Solution {
public:
    int candy(vector<int>& ratings) {
        int num = 0;
        vector<int> left(ratings.size(), 1);
        vector<int> right(ratings.size(), 1);
        for (int i = 1; i < ratings.size(); i++) {
            if (ratings[i] > ratings[i - 1]) {
                left[i] = left[i - 1] + 1;
            }
        }
        for (int i = ratings.size() - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                right[i] = right[i + 1] + 1;
            }
        }
        for (int i = 0; i < ratings.size(); i++) {
            num += max(left[i], right[i]);
        }
        return num;
    }
};
```