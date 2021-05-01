---
title: LeetCode 121
subtitle: "\"To form better habits or start new ones, focus on fixing one thing at a time.\""
date: 2020-03-30 06:48:58
tags:
---

### Algorithm: One Pass

Say the given array is:

**[7, 1, 5, 3, 6, 4]**

If we plot the numbers of the given array on a graph, we get:
### 思路

- 由于我们是想获取到最大的利润，我们的策略应该是低点买入，高点卖出。
- 由于题目对于交易次数有限制，只能交易一次，因此问题的本质其实就是求波峰浪谷的差值的最大值。

用图表示的话就是这样：

![idea](https://camo.githubusercontent.com/6c951edaf6d1af259e4eac1735a3a260e6a63708/68747470733a2f2f747661312e73696e61696d672e636e2f6c617267652f303038327a7962706c793167627837727a703965316a33306a67306332337a732e6a7067)
The points of interest are the peaks and valleys in the given graph. We need to find the largest peak following the smallest valley. We can maintain two variables - minprice and maxprofit corresponding to the smallest valley and maximum profit (maximum difference between selling price and minprice) obtained so far respectively.


##### Java Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        
        if (prices == null || prices.length == 0) return 0;
        int min = prices[0];
        int profit = 0;
        for ( int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                min = Math.min(prices[i - 1], min);
            }
            profit = Math.max(profit, prices[i] - min);
        }
        return profit;
    }
}
```

##### JS Code
```javascript
var maxProfit = function(prices) {
    let profit = 0;
    let min = prices[0];
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] > prices[i - 1]){
            min = Math.min(min, prices[i - 1])
        }
        profit = Math.max(profit, prices[i] - min) 
    }
    return profit;
};
```