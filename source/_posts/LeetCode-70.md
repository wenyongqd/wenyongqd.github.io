---
title: LeetCode 70
date: 2020-03-31 11:55:05
tags:
---

```java
class Solution {
    public int climbStairs(int n) {
        if (n <= 2) return n;
        int dp[] = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
}
```
