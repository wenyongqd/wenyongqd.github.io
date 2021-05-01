---
title: LeetCode 886
date: 2020-04-15 10:40:19
tags:
---
```java
class Solution {
    public boolean possibleBipartition(int N, int[][] dislikes) {
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        for (int[] e : dislikes) {
            int a = e[0], b = e[1];
            graph.computeIfAbsent(a, k -> new HashSet<>()).add(b);
            graph.computeIfAbsent(b, k -> new HashSet<>()).add(a);
        }
        
        int[] colors = new int[N + 1];
        for(int i = 1; i <= N; i++) {
            if (colors[i] == 0 && !dfs(graph, colors, i, 1)) return false;
        }
        return true;
    }
    
    
    private static boolean dfs(Map<Integer, Set<Integer>> graph, int[] colors, int pos, int c) {
        if (colors[pos] != 0) return colors[pos] == c;
        if (graph.get(pos) == null) return true;
        
        colors[pos] = c;
        for (int nei : graph.get(pos)) {
            if (!dfs(graph, colors, nei, -c)) return false;
        }
        return true;
    }
}
```