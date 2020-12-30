---
title: 'LeetCode 188. 买卖股票的最佳时机 IV(动态规划)(递归)'
date: 2020-12-28 15:55:43
tags: [算法,动态规划,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(4).jpg.webp
isTop: false
---
### 题目
给定一个整数数组 prices ，它的第 i 个元素 prices[i] 是一支给定的股票在第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
<!-- more -->
示例 1：
输入：k = 2, prices = [2,4,1]
输出：2
解释：在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。

示例 2：
输入：k = 2, prices = [3,2,6,5,0,3]
输出：7
解释：在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。

提示：

0 <= k <= 109
0 <= prices.length <= 1000
0 <= prices[i] <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
可以用递归来算，从根开始，要么买入，要么保持不动。
买入后可以进行的操作有卖出，保持不动
保持不动后的操作有：买入，保持不动
看成二叉树操作，把所有情况算出来(可以用一个备忘录记录下来已经算出来的值)
#### 方法1：递归(会超时)
```C++
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if (k == 0 || prices.size() == 0) {
            return 0;
        }
        return DFS(0, 0, 0, k, prices);
    }
    //计算k次交易，index表示当前是哪天，status是买卖状态，coutnt为交易次数
    int DFS(int index, int status, int count, int k, vector<int>& prices) {
        if (index == prices.size() || count == k) {
            return 0;
        }
        int keep = 0, sell = 0, buy = 0;
        //保持
        keep = DFS(index + 1, status, count, k, prices);
        if (status == 1) {
            //卖出
            sell = DFS(index + 1, 0, count + 1, k, prices) + prices[index];
        }
        else {
            //买入
            buy = DFS(index + 1, 1, count, k, prices) - prices[index];
        }
        return max(max(keep, sell), buy);
    }
};
```

#### 方法2：递归+记忆
```Java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if(prices==null || prices.length==0) {
            return 0;
        }
        int n = prices.length;
        //当k非常大时转为无限次交易
        if(k>=n/2) {
            int dp0=0,dp1=-prices[0];
            for(int i=1;i<n;++i) {
                int tmp = dp0;
                dp0 = Math.max(dp0,dp1+prices[i]);
                dp1 = Math.max(dp1,dp0-prices[i]);
            }
            return Math.max(dp0,dp1);
        }
        Map<Key,Integer> cache = new HashMap<Key,Integer>();
        return dfs(cache,0,0,0,k,prices);
    }

    //带记忆化的 计算k次交易，代码和递归版的一样只是前后加了缓存
    private int dfs(Map<Key,Integer> cache, int index, int status, int count, int k, int[] prices) {
        Key key = new Key(index,status,count);
        if(cache.containsKey(key)) {
            return cache.get(key);
        }
        if(index==prices.length || count==k) {
            return 0;
        }
        int a=0,b=0,c=0;
        a = dfs(cache,index+1,status,count,k,prices);
        if(status==1) {
            b = dfs(cache,index+1,0,count+1,k,prices)+prices[index];
        } else {
            c = dfs(cache,index+1,1,count,k,prices)-prices[index];
        }
        cache.put(key,Math.max(Math.max(a,b),c));
        return cache.get(key);
    }
    //Key对象封装了index、status、交易次数count，作为map的key
    private class Key {
        private final int index;
        private final int status;
        private final int count;
        Key(int index,int status,int count) {
            this.index = index;
            this.status = status;
            this.count = count;
        }
        //这里需要实现自定义的equals和hashCode函数
        public int hashCode() {
            return this.index + this.status + this.count;
        }
        public boolean equals(Object obj) {
            Key other = (Key)obj;
            if(index==other.index && status==other.status && count==other.count) {
                return true;
            }
            return false;
        }
    }
}
```