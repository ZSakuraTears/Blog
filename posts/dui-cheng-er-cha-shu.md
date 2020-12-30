---
title: '对称二叉树(二叉树)'
date: 2020-12-10 14:44:24
tags: [算法,LeetCode,二叉树]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(1).jpg.webp
isTop: false
---
### 题目
给定一个二叉树，检查它是否是镜像对称的。
<!-- more -->


例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

![](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/chrome_35r5gAjUVn.png)


但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

![](https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/chrome_BIOlXHyv1p.png)


进阶：

你可以运用递归和迭代两种方法解决这个问题吗？<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/symmetric-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
判断二叉树是否对称可以理解为判断一个节点的两个子树的里侧和外侧是否对称，就是后序遍历。
判断外侧是否对称，传入左节点的左孩子，右节点的右孩子。
判断里侧是否对称，传入左节点的右孩子，右节点的左孩子。
可以用递归挨个判断，所以递归函数传的值就要是left,right两个，想通这一点就好做了。
判断空的情况，
左空右空       返回true
左空右不空    返回false
左不空右空    返回false
最后是都不空，判断值
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
    bool cmp(TreeNode* left, TreeNode* right) {
        if (left == NULL && right == NULL) {
            return true;
        }
        else if (left == NULL && right != NULL) {
            return false;
        }
        else if (left != NULL && right == NULL) {
            return false;
        }
        //都不空判断值
        else if (left->val != right->val) {
            return false;
        }

        bool in = cmp(left->right, right->left);
        bool out = cmp(left->left, right->right);
        return in && out;
    }
    bool isSymmetric(TreeNode* root) {
        if (root == NULL) {
            return true;
        }
        return cmp(root->left, root->right);
    }
};
```