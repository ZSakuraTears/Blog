---
title: '切分木棒(DFS)(BFS)'
date: 2020-12-24 17:29:49
tags: [算法,搜索]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/PzudLoS8IG.jpg
isTop: false
---
### 题目
假设要把长度为 n 厘米的木棒切分为 1 厘米长的小段，但是 1 根木棒只能由 1 人切分，当木棒被切分为 3 段后，可以同时由 3 个人分别切分木棒（图 2）。
<!-- more -->
![图 2　n ＝ 8，m ＝ 3 的时候](http://www.ituring.com.cn/figures/2017/ProgrammerPuzzle/07.d01z.014.png)
求最多有 m 个人时，最少要切分几次。譬如 n ＝ 8，m＝ 3 时如图所示，切分 4 次就可以了。

作者：图灵教育
链接：https://leetcode-cn.com/leetbook/read/interesting-algorithm-puzzles-for-programmers/90ach5/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

### 思路
#### 方法1：DFS
```C++
#include <iostream>

using namespace std;

int sil(int m, int n, int num) //n要求段数  m人数 num目前段数
{
	if (num >= n) { //达到要求结束
		return 0;
	}
	else if (num < m) { //目前段数小于人数，直接段数*2
		return 1 + sil(m, n, num * 2);
	}
	else { //目前段数大于等于人数，增加m段
		return 1 + sil(m, n, num + m);
	}
}

int main()
{
	cout<<sil(3, 20, 1)<<endl<<sil(5, 100, 1);
	return 0;
}
```
#### 方法2：BFS
```C++
#include <iostream>

using namespace std;

int sil(int m, int n, int num) //n要求段数  m人数 num目前段数
{
	int count = 0;
	while (num < n) {
		num += num < m ? num : m;
        /*
		if (num < m) {
			num += num;
		}
		else {
			num += m;
		}
		count++;
		*/
		count++;
	}
	return count;
}

int main()
{
	cout<<sil(3, 20, 1)<<endl<<sil(5, 100, 1);
	return 0;
}
```