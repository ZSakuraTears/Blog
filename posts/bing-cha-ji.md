---
title: '朋友圈(并查集)'
date: 2020-12-02 19:02:21
tags: [算法,LeetCode,并查集]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/Zhao-Master/cdn/img/(4).jpg.webp
isTop: false
---
LeetCode547题 朋友圈
<!-- more -->
### 题目
班上有 N 名学生。其中有些人是朋友，有些则不是。他们的友谊具有是传递性。如果已知 A 是 B 的朋友，B 是 C 的朋友，那么我们可以认为 A 也是 C 的朋友。所谓的朋友圈，是指所有朋友的集合。<br><br>

给定一个 N * N 的矩阵 M，表示班级中学生之间的朋友关系。如果M[i][j] = 1，表示已知第 i 个和 j 个学生互为朋友关系，否则为不知道。你必须输出所有学生中的已知的朋友圈总数。<br><br><br>

 

示例 1：<br>
输入：
[[1,1,0],
 [1,1,0],
 [0,0,1]]<br><br>
输出：2 
解释：已知学生 0 和学生 1 互为朋友，他们在一个朋友圈。
第2个学生自己在一个朋友圈。所以返回 2 。<br><br>

示例 2：<br>
输入：
[[1,1,0],
 [1,1,1],
 [0,1,1]]<br><br>
输出：1
解释：已知学生 0 和学生 1 互为朋友，学生 1 和学生 2 互为朋友，所以学生 0 和学生 2 也是朋友，所以他们三个在一个朋友圈，返回 1 。<br><br>
 

提示：<br><br>

1 <= N <= 200
M[i][i] == 1
M[i][j] == M[j][i]<br><br>


来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/friend-circles
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。<br><br>

### 思路
运用并查集算出相关集合
#### 并查集不优化代码：
```C++
void union(int p, int q) {
    int rootP = find(p);
    int rootQ = find(q);
    if (rootP == rootQ)
        return;
    // 将两棵树合并为一棵
    parent[rootP] = rootQ;
    // parent[rootQ] = rootP 也一样
    count--; // 两个分量合二为一
}

/* 返回某个节点 x 的根节点 */
int find(int x) {
    // 根节点的 parent[x] == x
    while (parent[x] != x)
        x = parent[x];
    return x;
}

/* 返回当前的连通分量个数 */
int count() { 
    return count;
}
```
find函数是把一棵树直接接到另一棵树下面，这也就造成了树的退化(往链表退化)，就会使时间复杂度达到O(n)，union和connected都是要用到find，所以他们的时间复杂度也是O(n)。<br><br>
#### 优化方案
##### 平衡优化
另外开一个数组记录每棵树的“重量”(节点数),节点数少的接到节点数多的树里面，就可以降低复杂度。<br>
```C++
void union(int p, int q) {
    int rootP = find(p);
    int rootQ = find(q);
    if (rootP == rootQ)
        return;
    
    // 小树接到大树下面，较平衡
    if (size[rootP] > size[rootQ]) {
        parent[rootQ] = rootP;
        size[rootP] += size[rootQ];
    } else {
        parent[rootP] = rootQ;
        size[rootQ] += size[rootP];
    }
    count--;
}
```
<br>
##### 路径~~亚索~~压缩
如果我们可以进一步压缩树的高度，让树的高度始终为常数，那find的复杂度就是O(1).
压缩完是一个根节点下面都是叶子节点，这样树的高度就为常数，非常友好。<br><br>
```C++
int find(int x) {
    int r = x;
    while (parent[r] != r)
        r = parent[r]; //找到根节点
    int i = x, j;
    while (i != r) { //让每个节点都练到根节点上
        j = parent[i];
        parent[i] = r;
        i = j;
    }
    return r;
}
```
<br><br>
### 代码
```C++
class Solution {
public:
    int counts;
    vector<int> parent;
    vector<int> size;
    void UF(int n) {
        counts = n;
        for (int i = 0; i < n; i++) {
            parent.push_back(i);
            size.push_back(1);
        }
    }

    void Union(int p, int q) {
        int rootp = find(p);
        int rootq = find(q);
        if (rootp == rootq)
            return;
        if (size[rootp] > size[rootq]) {
            parent[rootq] = rootp;
            size[rootp] += size[rootq];
        }
        else {
            parent[rootp] = rootq;
            size[rootq] += size[rootp];
        }
        counts--;
    }

    int find(int x) {
        int r = x;
        while (parent[r] != r)
            r = parent[r];
        int i = x, j;
        while (i != r) {
            j = parent[i];
            parent[i] = r;
            i = j;
        }
        return r;
    }

    bool connected(int p, int q) {
        int rootp = find(p);
        int rootq = find(q);
        return rootp == rootq;
    }

    int count() {
        return counts;
    }

    int findCircleNum(vector<vector<int>>& M) {
        UF(M[0].size());
        for (int i = 0; i < M.size(); i++) {
            for (int j = 0; j < M[0].size(); j++) {
                if (M[i][j] == 1) {
                    Union(i, j);
                }
            }
        }
        return counts;
    }
};
```