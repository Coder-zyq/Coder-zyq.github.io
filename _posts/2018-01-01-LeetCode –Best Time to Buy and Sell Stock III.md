---
layout: post
title: 'LeetCode --Best Time to Buy and Sell Stock III'
subtitle: '15331404 张益强'
date: 2018-01-1
 
cover: 'https://leetcode.com/static/images/LeetCode_Sharing.png'
tags: 算法 LeetCode

---

# 

## LeetCode --Best Time to Buy and Sell Stock III

> 技术与社会生态的相互作用，使得技术发展经常带来更深远的问题，远远超出了技术设备的直接目的和运作本身，同样的技术，引入不同的环境，或在不同条件下，会带来非常不同的结果


[TOC]

----
### 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

至多交易2次，求最大利益。

### 算法解释
1. basically we want to maximize the formula: -price1 + price2 - price3 + price4, where every price appear in that order. So every time we visit a new price, we update the max possible value of 4 (partial) formula. That’s why we use max for each of the 4 states.
  也就是状态机4个状态。和cooldown相似。

在每个步骤中，我们可以看到，oneBuy始终是输入数组中的最低价格，oneBuyOneSell跟踪价格和最低价格之间的最大差异，TwoBuy的价值变化反映了输入价格数组中的谷底。
变量TwoBuyTwoSell保持直到目前的价格的最大的利润，
（代码比较清晰易懂，请看代码）

2. DP

> f[k, ii] represents the max profit up until prices[ii] (Note: NOT ending with prices[ii]) using at most k transactions.     





>    f[k, ii] = max(f[k, ii-1], prices[ii] - prices[jj] + f[k-1, jj]) { jj in range of [0, ii-1] }      
>     = max(f[k, ii-1], prices[ii] + max(f[k-1, jj] - prices[jj]))

```c++
      f[0, ii] = 0; 0 times transation makes 0 profit
      f[k, 0] = 0; if there is only one price data point you can't make any money no matter how many times you can trade
```

状态转移方程明了了，解释略

### 代码

```c++
public int maxProfit(int[] prices) {
    int oneBuy = Integer.MIN_VALUE;
    int oneBuyOneSell = 0;
    int twoBuy = Integer.MIN_VALUE;
    int twoBuyTwoSell = 0;
    for(int i = 0; i < prices.length; i++){
        oneBuy = Math.max(oneBuy, -prices[i]);//we set prices to negative, so the calculation of profit will be convenient
        oneBuyOneSell = Math.max(oneBuyOneSell, prices[i] + oneBuy);
        twoBuy = Math.max(twoBuy, oneBuyOneSell - prices[i]);//we can buy the second only after first is sold
        twoBuyTwoSell = Math.max(twoBuyTwoSell, twoBuy + prices[i]);
    }
    
    return Math.max(oneBuyOneSell, twoBuyTwoSell);
}
```

使用DP的方法

```c++
class Solution {
public:
    int maxProfit(vector<int> &prices) {
        
        if (prices.size() <= 1) return 0;
        else {
            int K = 2; // number of max transation allowed
            int maxProf = 0;
            vector<vector<int>> f(K+1, vector<int>(prices.size(), 0));
            for (int kk = 1; kk <= K; kk++) {
                int tmpMax = f[kk-1][0] - prices[0];
                for (int ii = 1; ii < prices.size(); ii++) {
                    f[kk][ii] = max(f[kk][ii-1], prices[ii] + tmpMax);
                    tmpMax = max(tmpMax, f[kk-1][ii] - prices[ii]);
                    maxProf = max(f[kk][ii], maxProf);
                }
            }
            return maxProf;
        }
    }
};
```

