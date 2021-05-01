---
title: LeetCode 39
date: 2020-04-19 07:51:47
tags:
---
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        backtrack(candidates, target, 0, res, new ArrayList<>());
        return res;
    }
    
    public void backtrack(int[]  candidates, int target, int start, List<List<Integer>> res, List<Integer> track) {
        if (target < 0) return;
        if (target == 0) res.add(new ArrayList<>(track));
        
        for (int i = start; i < candidates.length; i++) {
            track.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i, res, track);
            track.remove(track.size() - 1);
        }  
    }
}
```