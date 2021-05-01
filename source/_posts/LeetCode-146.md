---
title: LeetCode 146
date: 2020-03-17 11:26:13
subtitle: "\"If you really put a small value upon yourself, rest assured that the world will not raise your price.\"— Jean Sibelius"
tags: 
    - Java
    - LeetCode
---

## LeetCode *841*

### Catalog

1. [Tips](#Tips)
2. [Hints](#Hints)
3. [Code](#Code)

## Tips
This Java solution is an extended version of the the article published on the Discuss forum.

The problem can be solved with a hashmap that keeps track of the keys and its values in the double linked list. That results in **O(1)** time for put and get operations and allows to remove the first added node in **O(1)** time as well.

![figure](https://leetcode.com/problems/lru-cache/Figures/146/structure.png)
```java
class LRUCache {
    // 创建双向链表
    class Node {
        Node prev, next;
        int key, value;
        Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    Node head = new Node(0, 0), tail = new Node(0, 0);
    Map<Integer, Node> map = new HashMap<>();
    int max_len;
    public LRUCache(int capacity) {
        max_len = capacity;
        // 建立双链表
        head.next = tail;
        tail.prev = head;
    }
    public int get(int key) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            remove(node);
            add(node);
            return node.value;
        } else {
            return -1;
        }    
    }
    public void put(int key, int value) {
        if (map.containsKey(key)) {
            remove(map.get(key));
        }
        // 把表头位置节点删除(说明最近的数据值)
        if (map.size() == max_len) {
            remove(head.next);
        }
        add(new Node(key, value));
    }
    
    // 删除链表
    private void remove(Node node) {
        map.remove(node.key);
        // 删除节点
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    // 加在链表尾
    private void add(Node node) {
        map.put(node.key, node);
        Node pre_tail = tail.prev;
        node.next = tail;
        tail.prev = node;
        pre_tail.next = node;
        node.prev = pre_tail;
    }   
}
```

```java
class LRUCache {
    // 创建双向链表
    class Node {
        Node pre, next;
        int key, value;
    }

    private Node head, tail;
    private int max_len;
    private static HashMap<Integer, Node> map = new HashMap<>();
    
    LRUCache(int capacity) {
        head = new Node();
        tail = new Node();
        max_len = capacity;
    }
    
    public void put(int key, int value) {
        if (map.containsKey(key)) {
            map.remove(key);
        }
        if (map.size() == max_len) {
            if(max_len !=1 ){
               remove(tail);//删除尾部节点（最不常用） 
            }
            if(max_len == 1) {
                remove(head);
            }
            
        }
        Node newNode = new Node();
        newNode.key = key;
        newNode.value = value;
        add(newNode);
    }

    public int get(int key) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            remove(node);
            add(node);
            return node.value;
        } else {
            return -1;
        }
    }
    
    public void add(Node node) {
        map.put(node.key, node);

        if (tail.key != 0 && head.key != 0) {
            head.pre = node;
            node.next = head;
            head = head.pre;
            head.pre =  null;
        }
        if (max_len != 1) {
            if (head.key != 0 && tail.key == 0) {
                tail = head;
                head = node;
                head.next = tail;
                tail.pre = head;
                tail.next = null;
                head.pre = null;
            }
            if (head.key == 0) {
                head = node;
                head.next = tail;
                tail.pre = head;
                tail.next = null;
                head.pre = null;
            }
        }
        
        if (max_len == 1) {
            head = node;
            head.next = tail;
            tail.pre = head;
            tail.next = null;
            head.pre = null;
        }
    }
    
    //删除尾部节(最不常用)
    public void remove (Node node) {
        map.remove(node.key);
        if (tail.pre == head) {
            if (node == tail) {
                tail = new Node();
                tail.pre = head;
                head.next = tail;
                head.pre = null;
                tail.next = null;
            }
            if (node == head) {
                head = new Node();
                head.next = tail;
                tail.pre = head;
                head.pre = null;
                tail.next = null;
            } 
            
        } else {
            node.pre.next = node.next;
            node.next.pre = node.pre;
        }
    }
}
```