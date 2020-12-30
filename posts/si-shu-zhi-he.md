---
title: '四数之和（双指针）'
date: 2020-11-01 21:32:08
tags: [算法,LeetCode,双指针]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/54lqq0%20(1).jpg
isTop: false
---
#### 题目描述：
给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。<br><br>
<!-- more -->
注意：

答案中不可以包含重复的四元组。<br><br>

示例：

给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]<br><br>

来源：力扣18题（LeetCode）
链接：https://leetcode-cn.com/problems/4sum<br><br>
#### 题目分析
此题可以用双指针法解决，先用两个for循环i, j遍历前面，两个指针left, right收缩，当nums[i] + nums[j] + nums[left] + nums[right] == target 时，入数组，然后注意一下去重。（三数之和一个for循环，四数之和用两个，五数之和用三个......）<br><br>

#### 代码题解
```c++
vector<vector<int>> fourSum(vector<int> &nums, int target)
{
    vector<vector<int>> re;
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size(); i++)
    {
        if (i > 0 && nums[i] == nums[i - 1])//去重
            continue;
        for (int j = i + 1; j < nums.size(); j++)
        {
            if (j > i + 1 && nums[j] == nums[j - 1])//去重
                continue;
            int left = j + 1;
            int right = nums.size() - 1;
            while (left < right)
            {
                if (nums[i] + nums[j] + nums[left] + nums[right] > target)
                {
                    right--;
                }
                else if (nums[i] + nums[j] + nums[left] + nums[right] < target)
                {
                    left++;
                }
                else
                {
                    re.push_back(vector<int>{nums[i], nums[j], nums[left], nums[right]});//下面两个循环去重
                    while (right > left && nums[right] == nums[right - 1])
                    {
                        right--;
                    }
                    while (right > left && nums[left] == nums[left + 1])
                    {
                        left++;
                    }
                    //找到一个适合的后左右指针收缩
                    left++;
                    right--;
                }
            }
        }
    }
    return re;
}
```

