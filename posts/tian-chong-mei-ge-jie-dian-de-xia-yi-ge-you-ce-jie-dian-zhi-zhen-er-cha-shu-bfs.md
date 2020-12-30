---
title: '填充每个节点的下一个右侧节点指针(二叉树)(BFS)'
date: 2020-12-13 17:10:23
tags: [二叉树,算法,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/CV9awWXoCq.jpg
isTop: false
---
### 题目
给定一个 完美二叉树 ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：
<!-- more -->
struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。<br><br>

 

进阶：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。<br><br>

输入：root = [1,2,3,4,5,6,7]
输出：[1,#,2,3,#,4,5,6,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。序列化的输出按层序遍历排列，同一层节点由 next 指针连接，'#' 标志着每一层的结束。<br><br>
 

提示：

树中节点的数量少于 4096
-1000 <= node.val <= 1000<br><br>

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
每次循环用队列存储每一行的节点，每存储一个节点让前一个节点指向现在的节点。
每次循环队列弹一个，进两个。这样每次循环完队列把上一层的节点全部弹出，把新一层的节点全部加入。
```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if (root == NULL) {
            return NULL;
        }
        int num = 0;
        queue<Node*> q;
        q.push(root);
        while (!q.empty()) {
            Node* node;
            Node* front;
            front = NULL;
            num = q.size();
            for (int j = 0; j < num; j++) {
                node = q.front();
                q.pop();
                if (node->left != NULL)
                    q.push(node->left);
                if (node->right != NULL) 
                    q.push(node->right);
                if (front == NULL) {
                    front = node;
                }
                else {
                    front->next = node;
                    front = front->next;
                }
            };
        }
        return root;
    }
};
```