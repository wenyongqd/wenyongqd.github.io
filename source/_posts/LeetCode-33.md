---
title: LeetCode 33
date: 2020-04-02 08:47:22
tags:
---


```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        
        while (l <= r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] == target) return mid;
            if (nums[mid] >= nums[r]) {
                if (nums[mid] > target && nums[r] < target) r = mid;
                else l = mid + 1;
            }
            else {
                if (nums[mid] < target && nums[r] >= target) l = mid + 1;
                else r = mid;
            }
        }
        return -1;
    }
}
```
