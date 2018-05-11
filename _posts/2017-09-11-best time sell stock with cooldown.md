---
layout: post

title: 'LeetCode -Best Time to Buy and Sell Stock with Cooldown'

subtitle: '15331404 张益强'

date: 2017-09-11

cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'

tags: 算法 LeetCode
---

## LeetCode -Best Time to Buy and Sell Stock with Cooldown
[TOC]
### 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

- You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

- After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

**Example**

```

prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```
用一个数组表示股票每天的价格，数组的第i个数表示股票在第i天的价格。 如果某天卖了股票，那么第二天不能买股票，有一天的冷冻期。

### 算法解释
 状态机想法（discuss 大神）
![这里写图片描述](http://img.blog.csdn.net/20180113090109716?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ29kZXJfenlx/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

其中

> s0[i] = max(s0[i - 1], s2[i - 1]); // Stay at s0, or rest from s2
> s1[i] = max(s1[i - 1], s0[i - 1] - prices[i]); // Stay at s1, or buy from s0
> s2[i] = s1[i - 1] + prices[i]; // Only one way from s1

---

>  s0[0] = 0; // At the start, you don't have any stock if you just rest
>  s1[0] = -prices[0]; // After buy, you should have -prices[0] profit. Be positive!
>  s2[0] = 0; 

------
S1：buy[i]表示在第i天之前最后一个操作是买，此时的最大收益。

S2：sell[i]表示在第i天之前最后一个操作是卖，此时的最大收益。

S0：rest[i]表示在第i天之前最后一个操作是冷冻期，此时的最大收益。

---



### 代码

```c++
class Solution {
public:
	int maxProfit(vector<int>& prices){
		if (prices.size() <= 1) return 0;
		vector<int> s0(prices.size(), 0);
		vector<int> s1(prices.size(), 0);
		vector<int> s2(prices.size(), 0);
		s1[0] = -prices[0];
		s0[0] = 0;
		s2[0] = INT_MIN;
		for (int i = 1; i < prices.size(); i++) {
			s0[i] = max(s0[i - 1], s2[i - 1]);
			s1[i] = max(s1[i - 1], s0[i - 1] - prices[i]);
			s2[i] = s1[i - 1] + prices[i];
		}
		return max(s0[prices.size() - 1], s2[prices.size() - 1]);
	}
};
```

对意思进行理解优化后  

```c++
int maxProfit(vector<int>& prices) {
        if (prices.size() < 2) return 0;
        int rest = 0, buy = -prices[0], sell = 0;
        for (int i = 1; i < prices.size(); ++i) {
            int last_sell = sell;
            sell = buy + prices[i];
            buy = max(rest - prices[i], buy);
            rest = max(rest, last_sell);
        }
        return max(rest, sell);
    }
```

