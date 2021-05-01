---
title: LeetCode 46
date: 2020-04-17 21:42:39
tags:
---

```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        helper(nums, res, new ArrayList<>());
        return res;
    }
    
    public void helper(int[] nums, List<List<Integer>> res, List<Integer> track) {
        if (track.size() == nums.length) {
            res.add(new ArrayList<>(track));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (track.contains(nums[i]))
                continue;
            track.add(nums[i]);
            helper(nums, res, track);
            track.remove(track.size() - 1);
        }
    }
}
```