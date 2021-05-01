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
#### Algorithmd: Divide and Conquer

![devideandconquer](https://camo.githubusercontent.com/dfbf75bebf1618655527ed5dbb9f376a527d9817/68747470733a2f2f747661312e73696e61696d672e636e2f6c617267652f303038327a7962706c7931676276336867756961646a333134303075303434742e6a7067)

##### Algorithm

maxSubArray for array with n numbers:

1. If n == 1 : return this single element.
2. left_sum = maxSubArray for the left subarray, i.e. for the first n/2 numbers (middle element at index (left + right) / 2 always belongs to the left subarray).
3. right_sum = maxSubArray for the right subarray, i.e. for the last n/2 numbers.
4. cross_sum = maximum sum of the subarray containing elements from both left and right subarrays and hence crossing the middle element at index (left + right) / 2.
5. Merge the subproblems solutions, i.e. return max(left_sum, right_sum, cross_sum).

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums.length == 0 || nums == null) return 0;
        return helper(nums, 0, nums.length-1);
    }
    
    public int helper(int[] nums, int l, int r) {
        if (r < l) return Integer.MIN_VALUE;
        int mid = (r + l) >>> 1;
        int left = helper(nums, l, mid - 1);
        int right = helper(nums, mid + 1, r);
        int leftmax = 0;
        int rightmax = 0;
        int sum = 0;
        // left surfix maxSum start from index mid - 1 to l
        for (int i = mid - 1; i >= l; i--) {
            sum += nums[i];
            leftmax = Math.max(sum, leftmax);
        }
        // remember to let sum = 0
        sum = 0;
        // right prefix maxSum start from index mid + 1 to r
        for (int i = mid + 1; i <= r; i++) {
            sum += nums[i];
            rightmax = Math.max(sum, rightmax);
        }
        // max(left, right, crossSum)
        return Math.max(leftmax + nums[mid] + rightmax, Math.max(left, right));
    }
}
```
##### Complexity Analysis

- **Time complexity** : O(NlogN)


- **Space complexity** : O(logN) to keep the recursion stack.