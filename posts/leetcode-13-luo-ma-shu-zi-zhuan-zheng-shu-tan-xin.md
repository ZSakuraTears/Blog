---
title: 'LeetCode 13. 罗马数字转整数(贪心)'
date: 2020-12-26 14:16:39
tags: [算法,LeetCode,贪心]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/CV9awWXoCq.jpg
isTop: false
---
### 题目
罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。
<!-- more -->
通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

 

示例 1:

输入: "III"
输出: 3
示例 2:

输入: "IV"
输出: 4
示例 3:

输入: "IX"
输出: 9
示例 4:

输入: "LVIII"
输出: 58
解释: L = 50, V= 5, III = 3.
示例 5:

输入: "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.
 

提示：

题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。
IC 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。
关于罗马数字的详尽书写规则，可以参考 罗马数字 - Mathematics 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/roman-to-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
把罗马数字对应的整数存放到一个数组里，对s从头遍历，如果s[i] != reps[j][0]则j++，因为reps是字符串而且要判断的是首字母，所以是reps[j][0]。当s[i] == reps[j][0]时，还需要判断是不是特殊情况比如：四对应的IV，是对应的IX

`if (reps[j].size() > 1)`则说明reps当前对应的字符串属于特殊情况，`if (i < s.size() - 1 && s[i + 1] == reps[j][1])`说明s当前对应的数字与reps当前对应的数字相匹配，因为一个数占了两个字符所以要i++，j++。再把num累加。

`if (i < s.size() - 1 && s[i + 1] == reps[j][1])`不满足的情况有可能为s对应IV，reps对应IX，这样虽然前面的I相同但是后面的字符不相同，这种情况就让i不动（因为每次循环结束都会i++，所以先i--），j往后挪一个。

非特殊情况即`reps[j].size() <= 1`直接将num累加即可

```C++
class Solution {
public:
    int romanToInt(string s) {
        if (s.size() == 0) {
            return 0;
        }
        int values[]= {1000,900,500,400,100,90,50,40,10,9,5,4,1};
		string reps[]= {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        int j = 0, num = 0;
        for (int i = 0; i < s.size(); i++) {
            while (s[i] != reps[j][0]) {
                j++;
            }
            if (reps[j].size() > 1) {
                if (i < s.size() - 1 && s[i + 1] == reps[j][1]) {
                    i++;
                    num += values[j];
                    j++;
                }
                else {
                    i--;
                    j++;
                }
            }
            else {
                num += values[j];
            }
        }
        return num;
    }
};
```