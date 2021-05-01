---
title: LeetCode 78
date: 2020-04-16 18:29:14
tags:
---
```java
class Solution {
    List<List<Integer>> output = new ArrayList();
    
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list = IntStream.of(nums).boxed().collect(Collectors.toList());
        
        helper(list);
        return output;
    }
    
    public void helper(List<Integer> list) {
        if (list.size() == 0) {
            output.add(new ArrayList<>());
            return;
        }

        int n = list.get(list.size() - 1);
        list.remove(list.size() - 1);
        helper(list);

        int size = output.size();
        for (int i = 0; i < size; i++) {
            List<Integer> r = new ArrayList<>(output.get(i));
            output.add(r);
            output.get(output.size() - 1).add(n);
        }
    }
    
}

```