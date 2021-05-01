---
title: LeetCode 69
date: 2020-04-02 10:58:46
tags:
---
```java
class Solution {
    public int mySqrt(int x) {
        if (x <= 1) return x;
        int l = 1;
        int r = x;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if(mid == x / mid) return mid;
            else if(mid < x / mid) l = mid + 1;
            else r = mid;
        }
        return l - 1;
    }
}
```