---
title: LeetCode 84
date: 2020-04-01 20:34:00
tags:
---
```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int[] l = new int[n];
        int[] r = new int[n];
        Arrays.fill(l, -1);
        Arrays.fill(r, n);
        int ans = 0;
        
        for(int i = 1; i < n; i++) {
            int j = i - 1;
            while(j >= 0 && heights[i] <= heights[j]) 
                j = j - 1;
            l[i] = j;
        }
        for(int i = n - 2; i >= 0; i--) {
            int j = i + 1;
            while(j < n && heights[i] <= heights[j])
                j = j + 1;
            r[i] = j;
        }
        for(int i = 0; i < n; i++) {
            ans = Math.max(ans, heights[i] * (r[i] - l[i] - 1));
            System.out.println(ans);
        }
        return ans;
    }
}
```

```java
public class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length;
        int[] l = new int[n];
        int[] r = new int[n];
        Arrays.fill(l, -1);
        Arrays.fill(r, n);
        int ans = 0;
        
        for(int i = 1; i < n; i++) {
            int j = i - 1;
            while(j >= 0 && heights[i] <= heights[j]) 
                j = l[j];
            l[i] = j;
        }
        for(int i = n - 2; i >= 0; i--) {
            int j = i + 1;
            while(j < n && heights[i] <= heights[j])
                j = r[j];
            r[i] = j;
        }
        for(int i = 0; i < n; i++) {
            ans = Math.max(ans, heights[i] * (r[i] - l[i] - 1));
            System.out.println(ans);
        }
        return ans;
    }
}
```