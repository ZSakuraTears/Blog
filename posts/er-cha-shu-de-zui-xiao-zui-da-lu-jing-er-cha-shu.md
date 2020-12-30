---
title: '二叉树的最小(最大)路径(二叉树)'
date: 2020-12-13 13:54:14
tags: [二叉树,LeetCode,算法]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(8).jpg.webp
isTop: false
---
### 题目
给定一个二叉树，找出其最小深度。
最小深度是从根节点到最近叶子节点的最短路径上的节点数量。
说明：叶子节点是指没有子节点的节点。
<!-- more -->
 

示例 1：
输入：root = [3,9,20,null,null,15,7]
输出：2<br><br>

示例 2：
输入：root = [2,null,3,null,4,null,5,null,6]
输出：5<br><br>

提示：
树中节点数的范围在 [0, 105] 内
-1000 <= Node.val <= 1000<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-depth-of-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
二叉树每个节点的路径最小(最大)为左子树和右子树中最小(最大)路径加上它自己
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int minDepth(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }
        int left = minDepth(root->left);
        int right = minDepth(root->right);
        if (left == 0) {
            return right + 1;
        }
        if (right == 0) {
            return left + 1;
        }
        return min(left, right) + 1;
    }
};
```