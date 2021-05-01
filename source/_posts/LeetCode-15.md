---
title: LeetCode 15
date: 2020-03-31 07:36:35
tags:
---

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        HashSet<List<Integer>> result = new HashSet<List<Integer>>();
        if( nums != null && nums.length >= 3) {
            Arrays.sort(nums);
            int left, right;
            for(int i = 0; i < nums.length -2; i++) {
                left = i + 1;
                right = nums.length - 1;
                while(left < right) {
                    if(nums[left] + nums[right] == -nums[i]) {
                        result.add(new ArrayList<Integer>(Arrays.asList(nums[i], nums[left], nums[right])));
                        left++;
                        right--;
                    }
                    else if(nums[left] + nums[right] < -nums[i]) {
                        left++;
                    }
                    else right--;
                }
            }
        }
        return new ArrayList<List<Integer>>(result);
    }
}
```