---
title: LeetCode 303
date: 2020-03-31 12:27:26
tags:
---
```java
class NumArray {
    private int[] sum;
    public NumArray(int[] nums) {
        sum = new int[nums.length + 1];
        System.out.println(sum.toString());
        for (int i = 0; i < nums.length; i++) {
            sum[i + 1] = nums[i] + sum[i];

        }
    }
    // SR[i, j] = sum[j] - sum[i - 1]
    // i <= j
    public int sumRange(int i, int j) {     
        return sum[j + 1] - sum[i];
    }
}
```