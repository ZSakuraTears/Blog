---
title: '从前序与中序遍历序列构造二叉树(二叉树)'
date: 2020-12-12 12:26:26
tags: [二叉树,算法,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/PzudLoS8IG.jpg
isTop: false
---
### 题目
根据一棵树的前序遍历与中序遍历构造二叉树。
<!-- more -->
注意:
你可以假设树中没有重复的元素。

例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
和上一题基本一样0.0
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
    TreeNode* build(vector<int>& preorder, vector<int>& inorder) {
        TreeNode* tree = new TreeNode(preorder[0]);
        if (inorder.size() <= 1) {
            return tree;
        }
        int i, m;
        for (i = 0; i < inorder.size(); i++) {
            if (inorder[i] == preorder[0]) {
                break;
            }
        }
        m = i;
        vector<int> arr0, arr1, brr0, brr1;
        if (m == 0) {
            tree->left = NULL;
        }
        else {
            for (int j = 0, i = 1; j < m; j++, i++) {
                arr0.push_back(preorder[i]);
                brr0.push_back(inorder[j]);
            }
            tree->left = build(arr0, brr0);
        }
        if (m >= inorder.size() - 1) {
            tree->right = NULL;
        }
        else {
            for (int j = m + 1; j < inorder.size(); j++) {
                arr1.push_back(preorder[j]);
                brr1.push_back(inorder[j]);
            }
            tree->right = build(arr1, brr1);
        }
        return tree;
    }

    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (inorder.size() == 0 || preorder.size() == 0) {
            return NULL;
        }
        return build(preorder, inorder);
    }
};
```