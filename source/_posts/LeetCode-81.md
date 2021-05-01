---
title: LeetCode 81
date: 2020-04-04 10:14:51
tags:
---
```java
class Solution {
    public boolean search(int[] nums, int target) {
        int l = 0;
        int r = nums.length - 1;
        while (l <= r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] == target) return true;
            if (nums[mid] < nums[r]) {
                if (nums[mid] < target && nums[r] >= target ) l = mid + 1;
                else r = mid - 1;
            }
            else if (nums[mid] > nums[r]) {
                if (nums[l] <= target && nums[mid] > target) r = mid - 1;
                else l = mid + 1;
            }
            else r--;
        }
        return false;
    }
}
```