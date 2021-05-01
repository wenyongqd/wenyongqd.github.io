---
title: LeetCode 136
date: 2020-03-31 08:32:43
tags:
---

```java
class Solution {
    public int singleNumber(int[] nums) {
        int single_num = 0;
        for(int i = 0; i < nums.length; i++) {
            single_num = single_num ^ nums[i];
        }
        return single_num;
    }
}
```
