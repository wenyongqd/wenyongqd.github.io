---
title: LeetCode 802
date: 2020-04-13 08:55:05
tags:
---
```java
class Solution {
    public List<Integer> eventualSafeNodes(int[][] graph) {
        int[] color = new int[graph.length];
        List<Integer> res = new ArrayList<>();
        
        for (int i = 0; i < graph.length; i++) {
            if (!dfs(graph, i, color))
                res.add(i);
        }
        return res;
    }
    
    public boolean dfs(int[][] graph,int i, int[] color) {
        if (graph[i] == null || graph.length == 0) return false;
        
        color[i] = 1;
        for (int nei : graph[i]) {
            if (color[nei] == 1) return true;
            if (color[nei] == 0 && dfs(graph, nei, color)) return true;
        }
        
        color[i] = 2;
        return false;
    }
}
```