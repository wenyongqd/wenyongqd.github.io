---
title: LeetCode 668
date: 2020-04-06 08:53:00
tags:
---
```java
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int l = 1;
        int r = m * n;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            int cnt = 0;
            for (int i = 1; i <= m; i++) {
                cnt += mid > i*n ? n : mid / i;
            }
            if (cnt < k) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```