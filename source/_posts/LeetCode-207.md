---
title: LeetCode 207
date: 2020-04-10 17:29:32
tags:
---

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    int visited = 0;
    List<List<Integer>> adjList = new ArrayList<>();
    
    // create vertex entries
    for (int i = 0; i < numCourses; i++) {
        adjList.add(new ArrayList<Integer>());
    }
    int[] indegree = new int[numCourses];
    
    // Create adjacency list and indegree
    for (int i = 0; i < prerequisites.length; i++) {
        adjList.get(prerequisites[i][0]).add(prerequisites[i][1]);
        indegree[prerequisites[i][1]]++;
    }
            
    Queue<Integer> queue = new LinkedList<>();
    
    // Store indegree zero nodes into the queue
    for (int i = 0; i < indegree.length; i++) {
        if (indegree[i] == 0)
            queue.add(i);
    }
    
    // Perform BFS
    while (!queue.isEmpty()) {
        int vertex = queue.remove();
        List<Integer> neighbours = adjList.get(vertex);
        
        // Decrease indegree by 1 and check if we reached zero
        for (int i = 0; i < neighbours.size(); i++) {
            indegree[neighbours.get(i)]--;
            if (indegree[neighbours.get(i)] == 0) // If zero add to queue
                queue.add(neighbours.get(i));
        }
        visited++; // inc no of nodes visited
    }
    
    return visited == numCourses;
}
```