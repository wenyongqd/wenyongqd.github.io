---
title: LeetCode 122
date: 2020-03-30 08:05:16
tags:
---
### Approach: Peak Valley Approach
**Algorithm**

Say the given array is:

**[7, 1, 5, 3, 6, 4]**.

If we plot the numbers of the given array on a graph, we get:

**思路**

- 由于我们是想获取到最大的利润，我们的策略应该是低点买入，高点卖出。
- 由于题目对于交易次数没有限制，因此只要能够赚钱的机会我们都不应该放过。

If we analyze the graph, we notice that the points of interest are the consecutive valleys and peaks.

The key point is we need to consider every peak immediately following a valley to maximize the profit. In case we skip one of the peaks (trying to obtain more profit), we will end up losing the profit over one of the transactions leading to an overall lesser profit.
##### Java Code
```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1]) {
                profit = profit + prices[i] - prices[i - 1];
            }
        }
        return profit;
    }
}
```


##### JS Code 
```javascript
var maxProfit = function(prices) {
    let profit = 0;
    for (let i = 1; i < prices.length; i++) {
        if (prices[i] > prices[i - 1]) {
            profit = profit + prices[i] - prices[i - 1];
        }
    }
    return profit;
};
```