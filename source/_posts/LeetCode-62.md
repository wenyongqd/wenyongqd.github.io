---
title: LeetCode 62
date: 2020-03-31 12:54:30
tags:
---
```java
class Solution {
  public int uniquePaths(int m, int n) {
    int[][] d = new int[m][n];

    for(int[] arr : d) {
      Arrays.fill(arr, 1);
    }
    for(int i = 1; i < m; i++) {
        for(int j = 1; j < n; j++) {
            d[i][j] = d[i-1][j] + d[i][j-1];
        }
    }
    return d[m-1][n-1];
  }
}
```