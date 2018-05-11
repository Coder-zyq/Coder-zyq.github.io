---
layout: post

title: 'leetCode 解题报告之Counting Bits'

subtitle: '15331404 张益强'

date: 2018-04-18

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---

## leetCode 解题报告之Counting Bits
[TOC]

### 1. 题目描述  

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

就是尝试在O（n）的时间复杂度里，对某一个数进行判断：其二进制中1的数量，就是使用动态规划，参照前后关系，因为由于是0-n，所以前后关系是有的。

0 对应 ---0个1
1对应 ---1个1
2对应 ---1个1
3对应  ---2个1
4对应  ---1个1
5对应  ---2个1

-------

### 2. 解题思路描述
f（i）表示第i个数二进制中1的个数。

假设对某个数 n，
如果 n == 0； f（n）= 0;
如果n>=1 ;  f(n)与f（n-1），f(n-2),f(n-3)，。。。之间的关系是什么呢。

> **f[i] = f[i >> 1] + (i & 1);**
> 其实这里采用的是f（i）和f(i右移一位)的关系。例如 1111  ，右移之后就是111，那也就是计算了除了最后一位的1的个数，那么如果i%2 == 0，最后一位为0，结果就是f（右移一位）。如果是i%2==1，结果就是f（右移一位）+1，那就是f（i）=f（i>>1）+i%2.
> num is even: ret[num] = ret[num/2]
> num is odd: ret[num] = ret[(num -1) / 2] + 1
> so it can be reduced as: ret[i] = ret[i/2] + i % 2







> **f[i] = f[i&(i-1)] + 1;**
>  这里是另外一种思路，寻找一个一直是f（i） 少一个1的数。  存不存在呢。
>  事实上是存在的，是不是很厉害，这里都是这些打码的家伙会去研究这个东西了。。。那就是**i&(i-1)**
>  假如最后一位为1，显然i&(i-1)只和i 相差最后一位的1.  
>  假如最后一位不为1，为0，i-1 为偶数， i&i-1 刚好是去除最后一个一的结果。（膜）



### 3. 代码

```c++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> result(num+1, 0);
        for (int i = 1; i <= num; ++i)
            result[i] = result[i&(i-1)] + 1;
        return result;
    }
};
```



