---
title: LeetCode 162
date: 2020-04-05 09:41:39
tags:
---
```java
class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] < nums[mid + 1]) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```