---
title: LeetCode 42
subtitle: "\"The right mindset is about creating positive feedback loops.\""
mathjax: true
date: 2020-03-15 11:15:49
tags: 
    - Java
    - LeetCode
    - Dynamic Programming
---
## LeetCode *841*

### Catalog

1. [Tips](#Tips)
2. [Hints](#Hints)
3. [Code](#Code)

> **“Practice Is Everything.”**

![mindset](https://miro.medium.com/max/9752/1*BHjxLQHqV4FWEgI1SOdPQg.png)
<small class="img-hint">The right mindset is about creating positive feedback loops. **Jordan Peterson** talks about this in detail in his book **“12 Rules for Life”**.</small>


### Tips

### Hints
In brute force, we iterate over the left and right parts again and again just to find the highest bar size upto that index. But, this could be stored. Voila, dynamic programming.
![dynamic](https://leetcode.com/problems/trapping-rain-water/Figures/42/trapping_rain_water.png)

##### Algorithm

- Find maximum height of bar from the left end upto an index i in the array \text{left\_max}left_max.
- Find maximum height of bar from the right end upto an index i in the array \text{right\_max}right_max.
- Iterate over the \text{height}height array and update ans:
    - Add **min(max_left[i], max_right[i]) - height[i]** to ans


### Code

```java
class Solution {
    public int trap(int[] height) {
        int max =  0;
        int[] dp = new int[height.length];
        int result = 0;
        
        for (int i = 0; i < height.length; i++)  {
            max = Math.max(max, height[i]);
            dp[i] = max;
        }     
        max = 0;
        for (int i = height.length - 1; i >= 0; i--) {
            max = Math.max(max, height[i]);
            dp[i] = Math.min(max, dp[i]);
            if (i != 0 && i < height.length-1 && height[i] < dp[i]) {
                result += dp[i] - height[i];
            }
        }
        return result;
    }
}
```
---
### Complexity analysis
- Time complexity: O(n)
    - We store the maximum heights upto a point using 2 iterations of O(n) each.
    - We finally update \text{ans}ans using the stored values in O(n)O(n).
- Space complexity: O(n)O(n) extra space.
    - Additional O(n)O(n) space for **left_max** and **right_max** arrays than in Approach 1.