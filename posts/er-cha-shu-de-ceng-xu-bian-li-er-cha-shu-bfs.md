---
title: '二叉树的层序遍历(二叉树)(BFS)'
date: 2020-12-12 16:51:11
tags: [二叉树,LeetCode,算法]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/ycL3yPmxeH.jpg
isTop: false
---
### 题目
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。
<!-- more -->
 

示例：
二叉树：[3,9,20,null,null,15,7],
![](https://sakuratears.cn/post-images/1607763983990.png)

返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-level-order-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 解题思路
在用BFS循环遍历时。先记录现在队列里面的元素个数n，n就是此二叉树这一深度拥有的节点数，然后循环n次，把n个节点的左右孩子都添加到队列里面，每次循环完把队列前面的元素pop到一个动态数组里，这样就能实现一个深度的节点为一个数组了

### 代码

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
    vector<vector<int>> arr;

    void BFS(TreeNode* root) {
        queue<TreeNode*> brr;
        vector<int> crr;
        brr.push(root);
        int n = 0;
        while (!brr.empty()) {
            TreeNode* node = brr.front();
            n = brr.size(); //n记录当前队列元素个数
            for (int i = 0; i < n; i++) { //循环n次
                if (node->left != NULL) { //左孩子不为空则添加左孩子
                    brr.push(node->left);
                }
                if (node->right != NULL) { //右孩子不为空则添加右孩子
                    brr.push(node->right);
                }
                crr.push_back(brr.front()->val); //每次循环把队列的头元素的值添加到一个数组里
                brr.pop();
                node = brr.front(); //节点移动到下一个
            }
            arr.push_back(crr); //把当前数组元素添加到二维数组中
            crr.clear(); //当前数组清空
        }
    }

    vector<vector<int>> levelOrder(TreeNode* root) {
        if (root == NULL) {
            return arr;
        }
        BFS(root);
        return arr;
    }
};
```