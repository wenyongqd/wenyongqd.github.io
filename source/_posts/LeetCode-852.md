---
title: LeetCode 852
date: 2020-04-05 09:44:57
tags:
---
```java
class Solution {
    public int peakIndexInMountainArray(int[] A) {
        int l = 0;
        int r = A.length - 1;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (A[mid] < A[mid + 1]) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```