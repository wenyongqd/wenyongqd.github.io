---
title: LeetCode 378
date: 2020-04-03 11:51:24
tags:
---

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        if (matrix.length == 0) return 0;
        int start = matrix[0][0];
        int end = matrix[matrix.length - 1][matrix[0].length - 1];
        while (start <= end) {
            int mid = start + ((end - start) >> 1);
            int count = notGreaterCount(matrix, mid);
            if (count < k) start = mid + 1;
            else end = mid - 1;
        } 
        return start;
    }
    
    public int notGreaterCount(int[][] matrix, int target) {
        int curRow = 0;
        int COL_COUNT = matrix[0].length;
        int LAST_COL = COL_COUNT - 1;
        int res = 0;
        while (curRow < matrix.length) {
            if (target >= matrix[curRow][LAST_COL]) {
                res += COL_COUNT;
            } else {
                int i = COL_COUNT - 1;
                while(i >= 0 && target < matrix[curRow][i]) {
                    i--;
                }
                res += i + 1;
            }
            curRow++;
        }
        return res;
    }
}
```