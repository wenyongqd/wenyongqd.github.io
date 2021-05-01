---
title: LeetCode 1011
date: 2020-04-05 19:07:41
tags:
---
```java
class Solution {
    public int shipWithinDays(int[] weights, int D) {
        int l = Arrays.stream(weights).max().getAsInt();
        int r = 0;
        for ( int weight : weights) {
            r += weight;
        }
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            int d = 1;
            int cur = 0;
            for (int i = 0; i < weights.length; i++) {
                if (cur + weights[i] > mid) {
                    d++;
                    cur = 0;
                }
                cur += weights[i];
            }
            if ( d > D) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```