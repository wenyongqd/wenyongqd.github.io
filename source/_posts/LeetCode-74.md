---
title: LeetCode 74
date: 2020-04-02 13:09:49
tags:
---
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length == 0) return false;
        int l = 0;
        int row = matrix.length;
        int col = matrix[0].length;
        int r = row * col;
        
        while(l < r) {
            int mid = l + ((r - l ) >> 1);
            if (matrix[mid/col][mid%col] == target) return true;
            else if (matrix[mid/col][mid%col] < target) l = mid + 1;
            else r = mid;
        }
        return false;
    }
}
```