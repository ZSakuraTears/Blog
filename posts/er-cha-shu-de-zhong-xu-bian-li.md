---
title: '二叉树的中序遍历(二叉树)'
date: 2020-12-10 17:26:48
tags: [算法,二叉树,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(3).jpg.webp
isTop: false
---
### 题目
给定一个二叉树的根节点 root ，返回它的 中序 遍历。
<!-- more -->
 

示例 1：


输入：root = [1,null,2,3]
输出：[1,3,2]<br><br>
示例 2：

输入：root = []
输出：[]<br><br>
示例 3：

输入：root = [1]
输出：[1]<br><br>
示例 4：


输入：root = [1,2]
输出：[2,1]<br><br>
示例 5：


输入：root = [1,null,2]
输出：[1,2]<br><br>
 

提示：

树中节点数目在范围 [0, 100] 内
-100 <= Node.val <= 100<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-inorder-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
就二叉树的中序遍历，没有任何坑，直接写就行
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
    vector<int> arr;
    void traversal(TreeNode* root) {
        if (root == NULL) {
            return;
        }
        inorderTraversal(root->left);
        arr.push_back(root->val);
        inorderTraversal(root->right);
    }
    vector<int> inorderTraversal(TreeNode* root) {
        traversal(root);
        return arr;
    }
};
```