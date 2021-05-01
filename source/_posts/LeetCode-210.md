---
title: LeetCode 210
date: 2020-04-11 11:30:07
tags:
---
```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<Integer> result = new ArrayList<>();
        List<List<Integer>> adjList = new ArrayList<>();
        
        for (int i = 0; i < numCourses; i++) {
            adjList.add(new ArrayList<Integer>());
        }
        
        for (int i = 0; i < prerequisites.length; i++) {
            adjList.get(prerequisites[i][1]).add(prerequisites[i][0]);
        }
        
        int[] indegree = new int[numCourses];
        for (int i = 0; i < prerequisites.length; i++) {
            indegree[prerequisites[i][0]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < indegree.length; i++) {
            if (indegree[i] == 0)
                queue.add(i);
        }
        
        while(!queue.isEmpty()) {
            int vertex = queue.remove();
            result.add(vertex);
            List<Integer> neighbors = adjList.get(vertex);
            for (int i = 0; i < neighbors.size(); i++) {
                indegree[neighbors.get(i)]--;
                if (indegree[neighbors.get(i)] == 0) 
                    queue.add(neighbors.get(i));
            }
            
        }
        if (result.size() != numCourses) return new int[0];
        else
        return result.stream().mapToInt(Integer::valueOf).toArray();
    }
}




啊
```