---
title: '二叉树的序列化与反序列化(二叉树)'
date: 2020-12-15 08:23:20
tags: [二叉树,算法,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/yd8kqCqZwg.jpg
isTop: false
---
### 题目
序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。
<!-- more -->
请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

示例: 

你可以将以下二叉树：
```
      1
     / \
    2   3
       / \
      4   5
```
序列化为 "[1,2,3,null,null,4,5]"
提示: 这与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

说明: 不要使用类的成员 / 全局 / 静态变量来存储状态，你的序列化和反序列化算法应该是无状态的。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        queue<TreeNode*> q;
        q.push(root);
        string str = "";
        TreeNode* node;
        while (!q.empty()) {
            int n = q.size();
            for (int i = 0; i < n; i++) {
                node = q.front();
                q.pop();
                if (node == NULL) {
                    str += "null,";
                    continue;
                }
                str += to_string(node->val);
                str += ",";
                q.push(node->left);
                q.push(node->right);
            }
        }
        return str;
    }

    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if (data[0] == 'n') {
            return NULL;
        }
        int m = 0, n = 0;
        TreeNode* node;
        queue<TreeNode*> q;
        vector<int> arr;
        string str = "";
        while (m < data.size()) {
            if (data[m] == ',') {
                if (!str.empty())
                    arr.push_back(stoi(str));
                str = "";
                m++;
                continue;
            }
            if (data[m] == 'n') {
                m += 4;
                if (!str.empty())
                    arr.push_back(stoi(str));
                arr.push_back(-1024);
                str = "";
                continue;
            }
            str += data[m];
            m++;
        }
        TreeNode* root = new TreeNode(arr[0]);
        if (arr.size() == 1) {
            return root;
        }
        m = 1;
        q.push(root);
        while (!q.empty() && m < arr.size()) {
            n = q.size();
            for (int i = 0; i < n; i++) {
                node = q.front();
                q.pop();
                if (arr[m] != -1024) {
                    node->left = new TreeNode(arr[m]);
                    q.push(node->left);
                }
                else {
                    node->left = nullptr;
                }
                if (arr[m + 1] != -1024) {
                    node->right = new TreeNode(arr[m+1]);
                    q.push(node->right);
                }
                else {
                    node->right = nullptr;
                }
                m += 2;
            }
        }
        return root;
    }
};

// Your Codec object will be instantiated and called as such:
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```