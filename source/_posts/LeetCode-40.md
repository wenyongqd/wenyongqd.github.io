---
title: LeetCode 40
date: 2020-04-19 09:56:41
tags:
---
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(candidates);
        backtrack(candidates, target, 0, res, new ArrayList<>());
        return res;
    }
    
    public void backtrack(int[]  candidates, int target, int start, List<List<Integer>> res, List<Integer> track) {
        if (target < 0) return;
        if (target == 0) res.add(new ArrayList<>(track));
        
        for (int i = start; i < candidates.length; i++) {
            if (i > start && candidates[i] == candidates[i - 1])
                continue;
            track.add(candidates[i]);
            backtrack(candidates, target - candidates[i], i + 1, res, track);
            track.remove(track.size() - 1);
        }  
    }
}
```