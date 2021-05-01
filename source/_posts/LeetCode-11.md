---
title: LeetCode 11
date: 2020-03-30 10:34:46
tags:
---

```java
class Solution {
    
    // BF
    public int maxArea(int[] height) {
        int max = 0;
        for (int i = 0; i < height.length; i++) {
            for(int j = i + 1; j < height.length; j++){
                max = Math.max(max, Math.abs(j - i) * Math.min(height[j], height[i]));
            }
        }
        return max;
    }
}
```

```java
public class Solution {
    public int maxArea(int[] height) {
        int maxarea = 0, l = 0, r = height.length - 1;
        while (l < r) {
            maxarea = Math.max(maxarea, Math.min(height[l], height[r]) * (r - l));
            if (height[l] < height[r])
                l++;
            else
                r--;
        }
        return maxarea;
    }
}
```