---
layout: post

title: 'LeetCode --Best Time to Buy and Sell Stock II'

subtitle: '15331404 张益强'

date: 2018-02-02

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---

## Best Time to Buy and Sell Stock II

[TOC]

### 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

题目就是可以交易无限次数，此时的最大利益是多少。

### 算法解释

1. 第一种想法就是利用贪心算法。每次在diff为正的时候加起来。  
2. 即我们买入一个股票，当价格升高，我们等待一个价格即将下降的极点，然后卖出，这样我们就可以赚到最多的钱。
3. 反映到diff就是凡是元素为正，都可以在这个元素之前买入，在下一个元素为负的这个正元素卖出，即将所有正值加起来。
4. 例如 7 1 5 3 7 6 diff = 0 -6 4 -2 4 -1.
5. 所有正值相加就是8.也就是在1买入，5卖出，在3买入，在7卖出。结果刚好是8.
6. 再例如 1 2 3 4 5  6  diff = 0 1 1 1 1 1.结果就是5，在6卖出，1 买入。
### 代码

```c++
public int maxProfit(int[] prices) {
    int ret = 0;
    for (int i = 1 ; i < prices.length ; i++)
        ret += Math.max(prices[i] - prices[i-1] , 0);
    return ret;
}
```

