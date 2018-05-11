---
layout: post
title: 'LeetCode - kadane algorithm'
subtitle: '15331404 张益强'

date: 2018-03-03

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---

## LeetCode - kadane algorithm

[TOC]

----
### 题目描述

 [【max subArray】](https://leetcode.com/problems/maximum-subarray/description/)

[【Best Time to Buy and sell stock】](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)

### 
考虑向长度为i的数组里面插入第i+1 个数，即
maxSum（i+1） =max（插入第i+1个数，不插入第i+1个数）；

插入第i+1个数 的子序列和 = max（前i个数结尾的子序列之和+x，x）；

不插入第i+1个数的话，就是maxSum（i）.

所以归纳总结就是

```
public int max_subarray(int[] A){
 max_ending_here = max_so_far = 0;
 for(int n = 0; n < A.length; n++){
  max_ending_here = Math.max(max_ending_here + A[n], A[n]);
  max_so_far = Math.max(max_ending_here, max_so_far);
  }
 return max_so_far;
}
```
> 该算法关键在于，最大字片段中不可能包含求和指为负值的前缀。
>
>  所以在遍历过程中，每当累加结果成为一个非正值时， 就应当将下一个元素作为潜在最大子数列的起始元素， 重新开始累加。



------------------
### 对sell and buy stock补充

**只能买卖一次的情况求最大利益**
**就是diff只能选择一个最大和的子序列**

（用心思考）

一次买卖就是相当于定于一个起点和一个终点。
最大利益就是相邻差值的相加最大值。
所以也就是diff相加的子序列的和的最大值。

-----
（终结，继续膜）



