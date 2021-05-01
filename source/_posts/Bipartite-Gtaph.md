---
title: Bipartite Gtaph
date: 2020-04-15 07:47:11
tags:
---

```java
public class isBipartiteGraph {

    // Java program to find out whether
    // a given graph is Bipartite or not.
    // Using recursion.
    public static void main(String[] args) {
        //int[][] edges = new int[][]{{1, 2}, {1, 3}, {2, 4}};
        //int[][] edges = new int[][]{{1,2}, {2, 3}, {3, 4}, {4, 5}, {1, 5}};
        int[][] edges = new int[][]{{1, 5}, {1, 7}, {2, 5}, {3, 5}, {3, 6}, {4, 7}, {4, 8}};
        Map<Integer, Set<Integer>> graph = new HashMap<>();
        buildGraph(edges, graph);

        int N = 8;
        int[] colors = new int[N + 1];
        boolean isBipartit = isBipartite(graph, colors, N);
        System.out.println(isBipartit);
    }

    private static void buildGraph(int[][] edges, Map<Integer, Set<Integer>> graph) {
        for (int[] e : edges) {
            int a = e[0], b = e[1];
            graph.computeIfAbsent(a, k -> new HashSet<>()).add(b);
            graph.computeIfAbsent(b, k -> new HashSet<>()).add(a);
        }
    }

    private static boolean isBipartite(Map<Integer, Set<Integer>> graph, int[] colors, int N) {
        //有一个节点染色冲突就返回false
        for (int i = 1; i <= N; i++) {
            if (colors[i] == 0 && !dfs(graph, colors, i, 1)) return false;
        }
        //只有全部节点染色都不冲突，返回true
        return true;
    }

    // two colors 1 and -1
    // color this pos as c and
    // all its neighbours as -c
    //dfs的返回结果一次只验证一个节点
    private static boolean dfs(Map<Integer, Set<Integer>> graph, int[] colors, int pos, int c) {
        // if two adjacent are colored with same color then
        // the graph is not bipartite
        if (colors[pos] != 0) return colors[pos] == c;
        if (graph.get(pos) == null) return true;
        //上面的语句等于下面的语句
        //if (colors[pos] == c) return true;
        //if (colors[pos] == -c) return false;

        colors[pos] = c;
        for (int nei : graph.get(pos)) {
            // if the subtree rooted at vertex pos is not bipartite
            if (!dfs(graph, colors, nei, -c)) return false;
        }
        return true;
    }
}
```