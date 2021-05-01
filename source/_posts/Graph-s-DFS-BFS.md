---
title: Graph's DFS && BFS
date: 2020-04-08 11:23:54
tags:
---

```java
public void dfsRecursion(Graph graph, int source) {
    Node p;
    visited[i] = 1;
    p = graph.adjList[i].headNode;
    while (p != null) {
        //如果没有访问过，则递归
        if (visited[p.adjvex] == 0) {
            dfsRecursion(graph, p.adjvex);
        }
        p = p.nextNode;
    }
}
```