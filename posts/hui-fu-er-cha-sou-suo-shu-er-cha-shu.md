---
title: '恢复二叉搜索树(二叉树)'
date: 2020-12-16 19:44:46
tags: [二叉树,算法,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/ycL3yPmxeH.jpg
isTop: false
---
### 题目
给你二叉搜索树的根节点 root ，该树中的两个节点被错误地交换。请在不改变其结构的情况下，恢复这棵树。
<!-- more -->
进阶：使用 O(n) 空间复杂度的解法很容易实现。你能想出一个只使用常数空间的解决方案吗？<br><br>

 

示例 1：


输入：root = [1,3,null,null,2]
输出：[3,1,null,null,2]
解释：3 不能是 1 左孩子，因为 3 > 1 。交换 1 和 3 使二叉搜索树有效。<br><br>
示例 2：


输入：root = [3,1,4,null,null,2]
输出：[2,1,4,null,null,3]
解释：2 不能在 3 的右子树中，因为 2 < 3 。交换 2 和 3 使二叉搜索树有效。<br><br>
 

提示：

树上节点的数目在范围 [2, 1000] 内
-231 <= Node.val <= 231 - 1<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/recover-binary-search-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
二叉树搜索树中序遍历就是二叉搜索树元素从小到大排列，知道这个就好做了。
采用中序遍历：每个节点和前一个相比，小的话就把前一个节点记录下来(只有第一次记录前一个节点，因为题目说明只有两个元素错位)，然后下一次遇到前一个元素比后面的元素大的情况把后一个元素记录下来。
最后把两个记录点的val交换。
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
    TreeNode* pre = new TreeNode(-2147483648);
    TreeNode* s = NULL;
    TreeNode* t = new TreeNode();

    void recover(TreeNode* root) {
        if (root == NULL) {
            return;
        }
        recover(root->left);
        if (root->val < pre->val) {
            s = (s == NULL) ? pre:s;
            t = root; 
        }
        pre = root;
        recover(root->right);
    }
    void recoverTree(TreeNode* root) {
        recover(root);
        int n = s->val;
        s->val = t->val;
        t->val = n;
    }
};
```