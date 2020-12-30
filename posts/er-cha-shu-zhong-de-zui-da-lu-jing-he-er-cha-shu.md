---
title: '二叉树中的最大路径和(二叉树)(DFS)'
date: 2020-12-08 21:18:54
tags: [算法,LeetCode,二叉树,搜索]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(4).jpg.webp
isTop: false
---
### 题目
给定一个非空二叉树，返回其最大路径和。<br><br>
<!-- more -->
本题中，路径被定义为一条从树中任意节点出发，沿父节点-子节点连接，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。<br><br>

 

示例 1：

输入：[1,2,3]

       1
      / \
     2   3

输出：6<br><br>
示例 2：

输入：[-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出：42<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-maximum-path-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
每一个节点的最大路径是它左右子树中最大的路径加上它自己，这样就是先遍历左子树，再遍历右子树。
这样就是树的后序遍历+DFS的思想。
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
    int imax = INT_MIN;
    int maxpath(TreeNode* root) {
        if (root == nullptr) {
            return 0;
        }

        int left = max(0, maxpath(root->left));
        int right = max(0, maxpath(root->right));
        /*二叉树的后序遍历*/
        imax = max(imax, left + right + root->val);
        return max(left, right) + root->val;
    }
    int maxPathSum(TreeNode* root) {
        maxpath(root);
        return imax;
    }
};
```