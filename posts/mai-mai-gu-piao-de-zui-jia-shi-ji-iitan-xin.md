---
title: '买卖股票的最佳时机 II(贪心)'
date: 2020-11-12 20:22:38
tags: [算法,LeetCode,贪心]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(9).jpg.webp
isTop: false
---
#### 题目
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。
<!-- more -->
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。<br><br>

示例 1:
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。<br><br>

示例 2:
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。<br><br>

示例 3:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。<br><br>


提示：<br><br>

1 <= prices.length <= 3 * 10 ^ 4
0 <= prices[i] <= 10 ^ 4<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii<br><br>

####  思路
第一天买入，第三天卖出的利润是prices[3] - prices[1],也就是(prices[3] - prices[2]) + (prices[2] - porces[1])
可以发现，我们需要收集每天的正利润就可以，收集正利润的区间，就是股票买卖的区间，而我们只需要关注最终利润就可以了，不需要记录区间。<br><br>

**这就是贪心所贪的地方，只收集正利润。**<br><br>

![图](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/1604803105-SzWZhG-122.%E4%B9%B0%E5%8D%96%E8%82%A1%E7%A5%A8%E7%9A%84%E6%9C%80%E4%BD%B3%E6%97%B6%E6%9C%BAII.png)

#### 代码
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int result = 0;
        for (int i = 1; i < prices.size(); i++) {
            result += max(prices[i] - prices[i - 1], 0);
        }
        return result;
    }
};
```
<br><br><br>



思路借鉴作者：carlsun-2
链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/solution/122-mai-mai-gu-piao-de-zui-jia-shi-ji-iitan-xin-xi/
来源：力扣（LeetCode）