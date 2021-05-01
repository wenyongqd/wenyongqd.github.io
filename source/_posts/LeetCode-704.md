---
title: LeetCode 704
date: 2020-04-04 07:13:58
tags:
---
```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums.length == 0) return 0;
        int l = 0;
        int r = nums.length;
        
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] == target) return mid;
            else if (nums[mid] < target) l = mid + 1;
            else r = mid;
        }
        return -1;
    }
}
```