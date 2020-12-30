---
title: '二叉树的锯齿形层次遍历(二叉树)(BFS)'
date: 2020-12-15 17:01:22
tags: [二叉树,LeetCode,算法]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/gridea-zhu-ti-fog-geng-xin-ri-zhi.jpeg
isTop: false
---
### 题目
给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。<br><br>
<!-- more -->
例如：
给定二叉树 [3,9,20,null,null,15,7],
```
    3
   / \
  9  20
    /  \
   15   7
```
返回锯齿形层次遍历如下：

[
  [3],
  [20,9],
  [15,7]
]<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
首先把每一行所有节点存放到一个数组中，然后再把这个数组存放到一个二维数组中，然后把一维数组清空。依次遍历，然后每遍历完一行下一行数组翻转即可。
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
    bool jud = false; //判断因子，判断是否翻转
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> arr;
        vector<int> brr;
        if (root == NULL) {
            return arr;
        }
        queue<TreeNode*> q;
        q.push(root);
        TreeNode* node;
        while (!q.empty()) { //BFS
            int n = q.size(); //记录当前队列元素数量
            for (int i = 0; i < n; i++) {
                brr.push_back(q.front()->val); //把上一层所有节点加入到一维数组中
                node = q.front();
                q.pop();
                if (node->left != NULL) {
                    q.push(node->left);
                }
                if (node->right != NULL) {
                    q.push(node->right);
                }
            }
            if (jud == true) { //翻转
                reverse(brr.begin(), brr.end());
                jud = false; //更改反转因子
            }
            else { //不翻转
                jud = true; //更改反转因子
            }
            arr.push_back(brr); //把一维数组加入到二维数组
            brr.clear(); //然后把一维数组清空
        }
        return arr;
    }
};
```