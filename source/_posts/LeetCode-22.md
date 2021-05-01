---
title: LeetCode 22
date: 2020-04-20 13:05:42
tags:
---
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> res = new ArrayList<>();
        // int lc = 0, rc = 0;
        helper(n, 0, 0, res, "");
        return res;
    }
    
    public void helper(int n, int lc, int rc, List<String> res, String track ) {
        if (rc > lc || rc > n || lc > n) return;
        if (rc == lc && lc == n) {
            res.add(track);
            return;
        }
        
        helper(n, lc + 1, rc, res, track + "(");
        helper(n, lc, rc + 1, res, track + ")");
    }
}
```