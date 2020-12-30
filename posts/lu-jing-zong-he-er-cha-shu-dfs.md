---
title: '路径总和(二叉树)(DFS)'
date: 2020-12-13 15:52:49
tags: [二叉树,算法,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/Dl0g4BB4Fp.jpg
isTop: false
---
### 题目
给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。
<!-- more -->
说明: 叶子节点是指没有子节点的节点。<br><br>

示例: 
给定如下二叉树，以及目标和 sum = 22，
返回 true, 因为存在目标和为 22 的根节点到叶子节点的路径 5->4->11->2<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/path-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>
### 思路
从根节点开始遍历每个节点，每次递归将此根节点和前面路径的节点传入，然后当时叶子结点时判断总路径是否相等。
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool jud = false; //判断因子
    int num;
    void path(TreeNode* root, int n) {
        if (root == NULL) { //根为空的情况
            return;
        }
        //判断路径和是否相等，并且判断是否为叶子结点
        if (root->val + n == num && root->left == NULL && root->right == NULL) { 
            jud = true;
            return;
        }
        //递归遍历每个节点
        path(root->left, root->val + n);
        path(root->right, root->val + n);
    }
    bool hasPathSum(TreeNode* root, int sum) {
        //判断两者中特殊情况
        if (root == NULL && sum == 0) {
            return false;
        }
        if (root == NULL && sum != 0) {
            return false;
        }
        num = sum;
        path(root, 0);
        return jud;
    }
};
```