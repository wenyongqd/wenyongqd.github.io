---
title: LeetCode 719
date: 2020-04-04 09:13:48
tags:
---
```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
        Arrays.sort(nums);
        int l = 0;
        int r = nums[nums.length - 1] - nums[0];
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            int start = 0;
            int cnt = 0;
            for (int i = 0; i < nums.length; i++) {
                while (nums[i] - nums[start] > mid) start++;
                cnt += i - start;
            }
            if (cnt < k) l = mid + 1;
            else r = mid;
        }
        return l;
    }
}
```