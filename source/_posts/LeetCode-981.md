---
title: LeetCode 981
date: 2020-04-06 19:46:41
tags:
---
```java
class TimeMap {
    HashMap<String, TreeMap<Integer, String>> hm;
    
    /** Initialize your data structure here. */
    public TimeMap() {
        hm = new HashMap<>();
    }
    
    public void set(String key, String value, int timestamp) {
        hm.putIfAbsent(key, new TreeMap<>());
        hm.get(key).put(timestamp, value);
    }
    
    public String get(String key, int timestamp) {
        if(!hm.containsKey(key)){
            return "";
        }
        
        TreeMap<Integer, String> item = hm.get(key);
        Integer time = item.floorKey(timestamp);
        return time == null ? "" : item.get(time);
    }
}
```