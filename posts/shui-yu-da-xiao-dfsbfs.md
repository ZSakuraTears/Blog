---
title: '水域大小（DFS）（BFS）'
date: 2020-11-04 20:46:03
tags: [算法,LeetCode,搜索]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(8).jpg.webp
isTop: false
---
DFS BFS例题
<!-- more -->

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/pond-sizes-lcci<br><br>

你有一个用于表示一片土地的整数矩阵land，该矩阵中每个点的值代表对应地点的海拔高度。若值为0则表示水域。由垂直、水平或对角连接的水域为池塘。池塘的大小是指相连接的水域的个数。编写一个方法来计算矩阵中所有池塘的大小，返回值需要从小到大排序。<br><br>

示例：<br><br>

输入：
[
  [0,2,1,0],
  [0,1,0,1],
  [1,1,0,1],
  [0,1,0,1]
]
输出： [1,2,4]
提示：<br><br>

0 < len(land) <= 1000
0 < len(land[i]) <= 1000<br><br>

此题DFS，BFS都可以用。
(代码格式为leetcode模板格式)<br><br>

代码:
##### BFS
```C++
class Solution {
public:
    int n = 0;
    vector<vector<int>> dirs = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};//可以斜着所以是8个方向
    struct Node {int x; int y;};
    queue<Node> q;
    int BFS(int i, int j, vector<vector<int>>& land)
    {
        n = 1;
        Node start, node;
        start.x = i;
        start.y = j;
        land[i][j] = 1;
        q.push(start);
        while (!q.empty()) {
            start = q.front();
            q.pop();
            for (int i = 0; i < 8; i++)
            {
                node.x = start.x + dirs[i][0];
                node.y = start.y + dirs[i][1];
                if (node.x >= 0 && node.x < land.size() && node.y >= 0 && node.y < land[0].size() && land[node.x][node.y] == 0)//判断是否为鱼塘
                {
                    q.push(node);
                    land[node.x][node.y] = 1;//染色
                    n++;
                }
            }
        }
        return n;
    }

    vector<int> pondSizes(vector<vector<int>>& land) {
        vector<int> arr;
        for (int i = 0; i < land.size(); i++)
        {
            for (int j = 0; j < land[i].size(); j++)
            {
                if (land[i][j] == 0)
                {
                    arr.push_back(BFS(i, j, land));
                }
                else 
                {
                    continue;
                }
            }
        }
        sort(arr.begin(), arr.end());
        return arr;
    }
};
```
<br><br>
##### DFS
```C++
class Solution {
public:
    vector<vector<int>> dirs = {{-1, -1}, {-1, 0}, {-1, 1}, {0, -1}, {0, 1}, {1, -1}, {1, 0}, {1, 1}};
    struct Node {int x; int y;};
    
    int DFS(int i, int j, vector<vector<int>>& land)
    {
        if (i < 0 || i >= land.size() || j < 0 || j >= land[0].size()) return 0;
        if (land[i][j] != 0) return 0;//判断是否为鱼塘
        land[i][j] = 1;//染色
        Node next;
        int n = 1;
        for (int m = 0; m < 8; m++)
        {
            next.x = i + dirs[m][0];
            next.y = j + dirs[m][1];
            n += DFS(next.x, next.y, land);
        }
        return n;
    }

    vector<int> pondSizes(vector<vector<int>>& land) {
        vector<int> arr;
        for (int i = 0; i < land.size(); i++)
        {
            for (int j = 0; j < land[i].size(); j++)
            {
                if (land[i][j] == 0)
                {
                    arr.push_back(DFS(i, j, land));
                }
                else 
                {
                    continue;
                }
            }
        }
        sort(arr.begin(), arr.end());
        return arr;
    }
};
```

