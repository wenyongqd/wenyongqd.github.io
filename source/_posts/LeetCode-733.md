---
title: LeetCode 733
date: 2020-04-09 11:35:59
tags:
---
```java
class Solution {
    int[] dx = {1, -1, 0, 0};
    int[] dy = {0, 0, 1, -1};
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        if(image[sr][sc] == newColor){
            return image;
        }
        
        dfs(image, sr, sc, image[sr][sc], newColor);
        return image;
    }
    
    private void dfs(int [][] image, int i, int j, int oriColor, int newColor){
        if(i >= 0 && i < image.length && j >= 0 && j < image[0].length && image[i][j] == oriColor){
            image[i][j] = newColor;
            for (int k = 0; k < 4; k++) {
                dfs(image, i + dx[k], j + dy[k], oriColor, newColor);
            }
        }
    }
}
```