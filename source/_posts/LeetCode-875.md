---
title: LeetCode 875
date: 2020-04-03 07:55:55
tags:
---
```java
class Solution {
    public int minEatingSpeed(int[] piles, int H) {
        // Arrays.sort(piles);
        int l = 1;
        int r = Arrays.stream(piles).max().getAsInt();
        
        
        while(l <= r) {
            int k = l + ((r - l) >> 1);
            int curH = 0;
            for (int pile : piles) {
                curH += pile <= k ? 1 : (pile/k + 1);
            }
            if ( curH > H) l = k + 1;
            else r = k - 1;
        }
        return l;
    }
}
```