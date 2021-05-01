---
title: LeetCode 35
date: 2020-04-02 07:51:06
tags:
---


```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```