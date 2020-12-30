---
title: '寻找两个正序数组的中位数(分治)'
date: 2020-12-04 14:42:22
tags: [算法,分治,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/gridea-zhu-ti-fog-geng-xin-ri-zhi.jpeg
isTop: false
---
力扣的困难题~~极其简单！！！~~
<!-- more -->
### 题目
给定两个大小为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的中位数。<br><br>

进阶：你能设计一个时间复杂度为 O(log (m+n)) 的算法解决此问题吗？<br><br>

示例 1：
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2<br><br>

示例 2：
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5<br><br>

示例 3：
输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000<br><br>

示例 4：
输入：nums1 = [], nums2 = [1]
输出：1.00000<br><br>

示例 5：
输入：nums1 = [2], nums2 = []
输出：2.00000<br><br>
 

提示：<br><br>

nums1.length == m
nums2.length == n
0 <= m <= 1000
0 <= n <= 1000
1 <= m + n <= 2000
-106 <= nums1[i], nums2[i] <= 106<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/median-of-two-sorted-arrays
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
题目过于简单，把小的数组加到大的数组题然后sort，再找中位数。0.0<br><br>

### 代码
```C++
class Solution {
public:
    double median(vector<int> nums) {
        if (nums.size() % 2 == 0) {
            double dou0 = nums[nums.size() / 2];
            double dou1 = nums[nums.size() / 2 - 1];
            return (dou0 + dou1) / 2;
        }
        else {
            double dou0 = nums[nums.size() / 2];
            return dou0;
        }
    } 
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        if (nums1.size() == 0 && nums2.size() == 0)
            return 0;
        if (nums1.size() >= nums2.size()) {
            for (int i = 0; i < nums2.size(); i++) {
                nums1.push_back(nums2[i]);
            }
            sort(nums1.begin(), nums1.end());
            return median(nums1);
        }
        else {
            for (int i = 0; i < nums1.size(); i++) {
                nums2.push_back(nums1[i]);
            }
            sort(nums2.begin(), nums2.end());
            return median(nums2);
        }
    }
};
```