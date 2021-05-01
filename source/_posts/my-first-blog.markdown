---
layout: post
title: LeetCode 841
date: 2020-03-12 17:57:27
tags: 
    - Java
    - LeetCode
    - DFS
---

## LeetCode *841*

### Catalog

1. [Tips](#Tips)
2. [Hints](#Hints)
3. [Code](#Code)

> “Yeah It's on. ”

### Tips
#### ArrayList and HashSet 
- ArrayList allows duplicate values in its collection, HashSet doesn't allow to do that.
---

|No.           |Key         | ArrayList      | HashSet     |
| ----| ----------- | --------------------- | --------------------- |
| 1   | Implimentation       | ArrayList is the implementation of the list interface.       | HashSet on the other hand is the implementation of a set interface.      |
| 2   | Internal implimentation        | ArrayList internally implements array for its implementation.      | HashSet internally uses Hashmap for its implementation.       |
| 3   | Order of elements        | ArrayList maintains the insertion order i.e order of the object in which they are inserted.       | HashSet is an unordered collection and doesn't maintain any order.       |
| 4   | Duplicates        | ArrayList `allows duplicate` values in its collection.      | On other hand Hashset allows only one null value in its collection,after which no null value is allowed to be added.      |
| 5   | Index performance        | ArrayList uses index for its performance i.e its index based one can retrieve object by calling get(index) or remove objects by calling remove(index)      | HashSet is completely based on object also it doesn't provide get() method.      |
| 6   | Null Allowed        | Any number of null value can be inserted in arraylist without any restriction.       | On other hand Hashset allows only one null value in its collection,after which no null value is allowed to be added.       |
### Hints


### Code
```java
class Solution {
    public boolean canVisitAllRooms(List<List<Integer>> rooms) {
        //At the begining, we have a list "res" to store the keys we get..
        //that means at some point we have entered this room.
        Set<Integer> res = new HashSet<Integer>();
        helper(rooms, 0, res);
        res.add(0);
        //if any room that hasn't been visited, return false.
        for (int i = 0; i < rooms.size(); i++) {
            if (!res.contains(i)) return false;
        }
    return true; 
    }
    
    //When visiting a room for the first time, look at all the keys in the room.
    //For any key in the room that hasn't been used yet, add it to the list "res"
    public void helper(List<List<Integer>> rooms, int n, Set<Integer> res) {
        if ( rooms.get(n).size() == 0 ) return;
        for ( int i = 0; i < rooms.get(n).size(); i++) {
            if (res.contains(rooms.get(n).get(i))) continue;
            res.add(rooms.get(n).get(i));
            helper(rooms, rooms.get(n).get(i), res);
        }        
    }
}
```
### Complexity Analysis
- Time Complexity: O(N + E)O(N+E), where NN is the number of rooms, and EE is the total number of keys.
- Space Complexity: O(N)O(N) in additional space complexity, to store stack and seen.

> 很多时候，人们误以为自己需要的是具体的方法。但其实，真正需要切有用的是：一场顿悟，一场觉醒。那等价于一次基因突变。
