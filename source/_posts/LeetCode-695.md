---
title: LeetCode 695
date: 2020-04-09 08:27:10
tags:
---
```java
class Solution {
    int area = 0; 
    int[] dx = {0, 1, -1, 0};
    int[] dy = {-1, 0, 0, 1};
    public int maxAreaOfIsland(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int max = 0;
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                if (grid[i][j] == 1) {
                    helper(grid, i, j, m, n);
                    max = Math.max(max, area);
                    area = 0;
                }
            }
        }
        return max;
    }
    public void helper(int[][] grid, int x, int y, int m, int n) {
        if (x >= 0 && y >= 0 && x < m && y < n && grid[x][y] == 1) {    
            grid[x][y] = 0;
            area++;
            for (int k = 0; k < 4; k++) {
                helper(grid, x + dx[k], y + dy[k], m, n);
            }
        }      
    }
}
```