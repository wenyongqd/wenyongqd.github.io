---
title: LeetCode 53
subtitle: "\"Repetition is the mother of all learning.\""
date: 2020-03-28 11:12:03
tags:
    - LeetCode
---
### Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

> **Input**: [-2,1,-3,4,-1,2,1,-5,4],
  **Output**: 6
  **Explanation**: [4,-1,2,1] has the largest sum = 6. 

**Follow up:**

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

#### Algorithm - Prefix Sum + Brute force
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int max = Integer.MIN_VALUE;
        int sum1 = 0;
        if (nums.length == 1) return nums[0];
        for ( int i = 0; i < nums.length; i++) {
            sum1 = sum1 + nums[i];
            int sum2 = 0;
            for ( int j = 0; j <= i; j++) {              
                int prefixSum = sum1 - sum2;
                max = Math.max(max, prefixSum);
                sum2 = sum2 + nums[j];
                max = Math.max(max, prefixSum);
            }
        }
        return max;
    }
}
```
#### Algorithm: PrefixSum + Brute force(Improved)
```java
class MaximumSubarrayPrefixSum {
  public int maxSubArray(int[] nums) {
      int len = nums.length;
      int maxSum = Integer.MIN_VALUE;
      int sum = 0;
      for (int i = 0; i < len; i++) {
        sum = 0;
        for (int j = i; j < len; j++) {
          sum += nums[j];
          maxSum = Math.max(maxSum, sum);
        }
      }
      return maxSum;
  }
}
```


### Complexity analysis
- **Time complexity**: O(n^2)
    - n is the length of array.
- **Space complexity**: O(n) extra space.
    - the array space od prefixSum is n
    
#### Algorithmd: Advanced PrefixSum

**Tips:**
1. <font color="red">**max should compare with nums[0].**</font>
> What if the input array is [-1, -2, -3].
> What if the imput array is [1, 2, 3].
 
 
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = 0;
        int sumMin = 0;
        int max = nums[0];

        for ( int num : nums) {
            sum = sum + num;
            max = Math.max(max, sum - sumMin );
            sumMin = Math.min(sumMin, sum);            
        }
        return max;
    }
}
```