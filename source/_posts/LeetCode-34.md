---
title: LeetCode 34
date: 2020-04-03 13:36:09
tags:
---

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        int[] res = new int[2];
        Arrays.fill(res, -1);
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        if (nums.length == 0 || nums[l] != target) return res;
        res[0] = l;
        r = nums.length - 1;
        while (l < r) {
            int mid = l + ((r - l) >> 1) + 1;
            if (nums[mid] <= target) l = mid;
            else r = mid - 1;
        }
        res[1] = l;
        return res;
    }
}
```