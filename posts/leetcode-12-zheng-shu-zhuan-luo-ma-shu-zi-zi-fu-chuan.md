---
title: 'LeetCode 12. 整数转罗马数字(字符串)(贪心算法)'
date: 2020-12-22 19:15:18
tags: [算法,贪心,字符串,LeetCode]
published: true
hideInList: false
feature: https://cdn.jsdelivr.net/gh/ZSakuraTears/cdn/img/Dl0g4BB4Fp.jpg
isTop: false
---
### 题目
罗马数字包含以下七种字符： I， V， X， L，C，D 和 M。

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
给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。

示例 1:

输入: 3
输出: "III"
示例 2:

输入: 4
输出: "IV"
示例 3:

输入: 9
输出: "IX"
示例 4:

输入: 58
输出: "LVIII"
解释: L = 50, V = 5, III = 3.
示例 5:

输入: 1994
输出: "MCMXCIV"
解释: M = 1000, CM = 900, XC = 90, IV = 4.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/integer-to-roman
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 思路
#### 方法1:暴力解法
把每种情况都写出来然后直接暴力解决
```C++
class Solution {
public:
    string five(int num) {
        string str;
         if (num == 4) {
                str = "IV";
        }
        else if (num == 5) {
            str = "V";
        }
        else {
            for (int i = 0; i < num; i++) {
                str += 'I';
            }
        }
        return str;
    }

    string ten(int num) {
        string str;
        if (num == 9) {
            str = "IX";
        }
        else if (num == 10) {
            str = "X";
        }
        else {
            str = "V";
            for (int i = 0; i < num - 5; i++) {
                str += 'I';
            }
        }
        return str;
    }

    string fifty(int num) {
        string str;
        if (num == 40) {
            str = "XL";
        }
        else if (num == 50) {
            str = "L";
        }
        else if (num > 40) {
            str = "XL";
            int n = num - 40;
            if (n > 5) {
                str += ten(n);
            }
            else {
                str += five(n);
            }
        }
        else {
            int n = num / 10;
            num %= 10;
            for (int i = 0; i < n; i++) {
                str += 'X';
            }
            if (num <= 5) {
                str += five(num);
            }
            else {
                str += ten(num);
            }
        }
        return str;
    }

    string hundred(int num) {
        string str;
        if (num == 90) {
            str = "XC";
        }
        else if (num == 100) {
            str = "C";
        }
        else if (num > 90) {
            str = "XC";
            int n = num - 90;
            if (n > 5) {
                str += ten(n);
            }
            else {
                str += five(n);
            }            
        }
        else {
            str = "L";
            num -= 50;
            int n = num / 10;
            num %= 10;
            for (int i = 0; i < n; i++) {
                str += 'X';
            }
            if (num <= 5) {
                str += five(num);
            }
            else {
                str += ten(num);
            }            
        }
        return str;
    }

    string fiveh(int num) {
        string str;
        if (num == 400) {
            str = "CD";
        }
        else if (num == 500) {
            str = "D";
        }
        else if (num > 400) {
            str = "CD";
            int n = num - 400;
            if (n > 50) {
                str += hundred(n);
            }
            else {
                str += fifty(n);
            }
        }
        else {
            int n = num / 100;
            num %= 100;
            for (int i = 0; i < n; i++) {
                str += 'C';
            }
            if (num > 50) {
                str += hundred(num);
            }
            else {
                str += fifty(num);
            }
        }
        return str;
    }

    string thousand(int num) {
        string str;
        if (num == 900) {
            str = "CM";
        }
        else if (num == 1000) {
            str = "M";
        }
        else if (num > 900) {
            str = "CM";
            int n = num - 900;
            // cout<<num;
            if (n > 50) {
                str += hundred(n);
            }
            else {
                str += fifty(n);
            }
        }
        else {
            str = "D";
            num -= 500;
            int n = num / 100;
            num %= 100;
            // cout<<num;
            for (int i = 0; i < n; i++) {
                str += "C";
            }
            if (num > 50) {
                str += hundred(num);
            }
            else {
                // cout<<num<<" "<<fifty(num);
                str += fifty(num);
            }
        }
        return str;
    }

    string more(int num) {
        string str;
        int n = num / 1000;
        num %= 1000;
        for (int i = 0; i < n; i++) {
            str += "M";
        }
        if (num <= 5) {
            str += five(num);
        }
        else if (num <= 10) {
            str += ten(num);
        }
        else if (num <= 50) {
            str += fifty(num);
        }
        else if (num <= 100) {
            str += hundred(num);
        }
        else if (num <= 500) {
            str += fiveh(num);
        }
        else if (num <= 1000) {
            str += thousand(num);
        }
        return str;
    }

    string intToRoman(int num) {
        string str = "";
        if (num > 0) {
            if (num <= 5) {
                str += five(num);
            }
            else if (num <= 10) {
                str += ten(num);
            }
            else if (num <= 50) {
                str += fifty(num);
            }
            else if (num <= 100) {
                str += hundred(num);
            }
            else if (num <= 500) {
                str += fiveh(num);
            }
            else if (num <= 1000) {
                str += thousand(num);
            }
            else {
                str += more(num);
            }
        }
        else {
            str = "";
        }
        return str;
    }
};
```
#### 方法2:贪心算法
把阿拉伯数字与罗马数字可能出现的所有情况和对应关系，放在两个数组中，并且按照阿拉伯数字的大小降序排列。每次尽可能优先使用较大数值对应的字符
```C++
class Solution {
public:
	string intToRoman(int num) {
		int values[]= {1000,900,500,400,100,90,50,40,10,9,5,4,1};
		string reps[]= {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
		string res;
		for(int i=0; i<13; i++) {
			while(num>=values[i]) {
				num -= values[i];
				res += reps[i];
			}
		}
		return res;
	}
};
```