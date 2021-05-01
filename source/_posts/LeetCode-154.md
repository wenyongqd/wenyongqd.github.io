---
title: LeetCode 154
date: 2020-04-05 09:09:25
tags:
---
```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] > nums[r]) l = mid + 1;
            else if (nums[mid] < nums[r]) r = mid;
            else r--;
        }
        return nums[l];
    }
}
```