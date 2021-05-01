---
title: LeetCode 547
date: 2020-04-08 19:24:58
tags:
---

```java
class Solution {
    public int findCircleNum(int[][] M) {  
        int n = M.length;
        boolean [] visited = new boolean[n];
        int res = 0;
        for(int i = 0; i<n; i++){
            if(!visited[i]){
                dfs(M, visited, i);
                res++;
            }
        }
        return res;
    }
    
    private void dfs(int [][] M, boolean [] visited, int i){
        for(int j = 0; j<M[0].length; j++){
            if(!visited[j] && M[i][j]==1){
                visited[j] = true;
                dfs(M, visited, j);
            }
        }
    }
}
```