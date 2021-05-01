---
title: LeetCode 47
date: 2020-04-19 12:54:53
tags:
---
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if (nums.length < 1) return res;
        Arrays.sort(nums);
        helper(nums, res, new ArrayList<Integer>(), new boolean[nums.length]);
        return res;
    }
    
    public void helper(int[] nums, List<List<Integer>> res, List<Integer> track, boolean[] visited) {
        if (track.size() == nums.length) {
            res.add(new ArrayList<>(track));
            return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (visited[i]) continue;
            if (i > 0 && nums[i] == nums[i - 1] && !visited[i - 1]) continue;
            // if (track.contains(nums[i])) continue;
            visited[i] = true;
            track.add(nums[i]);
            helper(nums, res, track, visited);
            track.remove(track.size() - 1);
            visited[i] = false;
        }
    }
}
```