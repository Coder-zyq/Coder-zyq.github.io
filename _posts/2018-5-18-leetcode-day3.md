---
layout: post
title: 'LeetCode day 3-ZigZag Conversion'
subtitle: ' coder-zyq'
date: 2018-05-18
categories: LeetCode  
cover: 'http://img.article.pchome.net/00/34/54/50/pic_lib/wm/Black04.jpg'
tags: LeetCode C++ algorithm

---

# ZigZag Conversion

## 题目描述
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```c
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

```c
string convert(string s, int numRows);
```
Example 1:

```c
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```
Example 2:

```c
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```
## 解析
把字符串按照z字型排列，源字符串为0123456789
nRows=3变为了0481357926
nRows=4变为了0615724839

| 0    |      | 4    |      | 8    |
| ---- | ---- | ---- | ---- | ---- |
| 1    | 3    | 5    | 7    | 9    |
| 2    |      | 6    |      |      |

|  0   |      |      |  6   |
| :--: | :--: | :--: | :--: |
|  1   |      |  5   |  7   |
|  2   |  4   |      |  8   |
|  3   |      |      |  9   |

(1)第一行和最后一行下标间隔都是interval = nRows*2-2 = 8 ;                                             

(2)中间行的间隔是周期性的,第i行的间隔是: interval–2i,  2i,  interval–2i, 2i, interval–2i, 2i, …




## 解答

```c
class Solution {
public:
    string convert(string s, int nRows) {
    	int l = s.size();
    	if(nRows == 1) return s;
    	string result =s;
    	int interval = nRows*2-2;
    	int k= 0;//下标
    	for(int j=0;j<l;j+=interval){
    		result[k++]=s[j];
    	}

    	//第j行
    	for(int j=1;j<nRows-1;j++){
    		int inter_s = 2*j;
    		int d = 1;
            int inter=inter_s;
    		for(int i = j; i < l; i+=inter){
    			result[k++] = s[i];
    			if(d ==1){
    			    inter = interval -inter_s;
    			    d=0;
                }else if(d==0) {
    			inter = inter_s;
                    d=1;
    			}
    		}


    	}


    	for(int j= nRows-1; j<l;j+=interval){
    		result[k++]=s[j];
    	}
    	return result;
    }
};
```

## 大神解答

1. 为每一行构造一个相应的string，往里面添加元素，所有将这些string   append起来。必要点：清空string数组。

   ```c
   string convert(string s, int nRows) {
       
       if (nRows <= 1)
           return s;
   
       const int len = (int)s.length();
       string *str = new string[nRows];
   
       int row = 0, step = 1;
       for (int i = 0; i < len; ++i)
       {
           str[row].push_back(s[i]);
   
           if (row == 0)
               step = 1;
           else if (row == nRows - 1)
               step = -1;
   
           row += step;
       }
   
       s.clear();
       for (int j = 0; j < nRows; ++j)
       {
           s.append(str[j]);
       }
   
       delete[] str;
       return s;
   }
   ```

   

2. 还有一个循环这种想法的，一个cycle = 2*nRows - 2

   对第一行特殊处理，然后每一个cycle，一行会添加两个数。求出这两个数的规律即可。

   ```c
   j = i + cycle*k, k = 0, 1, 2, ...    //the current row is i, the index of //the first element is j:
   secondJ = (j - i) + cycle - i // index of the second element is secondJ
   ```