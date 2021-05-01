---
title: LeetCode 216
date: 2020-04-19 10:29:59
tags:
---
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> res = new ArrayList<>();
        helper(k, n, res, new ArrayList<Integer>(), 1);
        return res;
    }
    
    public void helper(int k, int n, List<List<Integer>> res, List<Integer> track, int start) {
        if (n < 0) return;
        if (k == 0 && n == 0) res.add(new ArrayList<>(track));
        
        for (int i = start; i <= 9; i++) {
            // if (i > n) return;
            track.add(i);
            helper(k - 1, n - i, res, track, i + 1);
            track.remove(track.size() - 1);
        }
    }
}
```