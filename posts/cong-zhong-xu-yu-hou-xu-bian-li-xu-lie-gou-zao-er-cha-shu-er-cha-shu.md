---
title: '从中序与后序遍历序列构造二叉树(二叉树)'
date: 2020-12-11 20:51:54
tags: [算法,二叉树,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/gridea-zhu-ti-fog-geng-xin-ri-zhi.jpeg
isTop: false
---
### 题目
根据一棵树的中序遍历与后序遍历构造二叉树。
<!-- more -->
注意:
你可以假设树中没有重复的元素。<br><br>

例如，给出
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]<br><br>

得到结果：[3,9,20,null,null,15,7]<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
二叉树的后序遍历最后一个元素是二叉树的的根节点，然后中序遍历根节点左边元素是左子树的节点，右边是右子树的节点。
知道这个这道题就很简单了，用递归调用求左子树右子树。
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
    TreeNode* build(vector<int>& inorder, vector<int>& postorder) {
        TreeNode* tree = new TreeNode(postorder[postorder.size() - 1]);
        if (inorder.size() <= 1) {
            return tree;
        }
        int i, m; //找到根节点m
        for (i = 0; i < inorder.size(); i++) {
            if (inorder[i] == postorder[postorder.size() - 1]) {
                break;
            }
        }
        m = i;
        vector<int> arr0, arr1, brr0, brr1;
        if (m == 0) { //考虑左边已经空了的情况
            tree->left = NULL;
        }
        else {
            for (int i = 0; i < m; i++) {
                arr0.push_back(inorder[i]);
                brr0.push_back(postorder[i]);
            }
            tree->left = build(arr0, brr0);
        }
        if (m >= inorder.size() - 1) {  //考虑右边已经空了的情况
            tree->right = NULL;
        }
        else {
            for (int i = m + 1, j = m; i < inorder.size(); i++, j++) {
                arr1.push_back(inorder[i]);
                brr1.push_back(postorder[j]);
            }
            tree->right = build(arr1, brr1);
        }
        return tree;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if (inorder.size() == 0 || postorder.size() == 0) {
            return NULL;
        }
        return build(inorder, postorder);
    }
};
```