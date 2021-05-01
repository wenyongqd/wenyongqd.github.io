---
title: Linked List Questions
date: 2020-07-17 23:34:34
tags:
---

### 237. Delete Node in a Linked List <font color=green><Easy\></font>

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.
Given linked list -- head = [4,5,1,9], which looks like following:

![image](https://assets.leetcode.com/uploads/2018/12/28/237_example.png)

**Example 1:**

> **Input: head** = [4,5,1,9], node = 5
> **Output:** [4,1,9]
> **Explanation:** You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        if (node.next == null) {
            node = null;
            return;
        }

        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

### 206. Reverse Linked List <font color=green><Easy\></font>

Reverse a singly linked list.

**Example:**

> **Input:** 1->2->3->4->5->NULL
> **Output:** 5->4->3->2->1->NULL

![image](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0206-Reverse-Linked-List/Animation/Animation.gif)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;

        while (cur != null) {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```

### 92. Reverse Linked List II

Reverse a linked list from position m to n. Do it in one-pass.
**Note:** 1 ≤ m ≤ n ≤ length of list.
**Example:**
>**Input:** 1->2->3->4->5->NULL, m = 2, n = 4
**Output:** 1->4->3->2->5->NULL
![image](https://upload-images.jianshu.io/upload_images/14030231-ca0192c24490c1fb.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    // 前驱节点
    ListNode prev = dummy;
    // 反转区间开始节点
    ListNode start = head;
    // 反转区间结束节点
    ListNode end = head;
    // 后继节点
    ListNode successor;
    // 第一个for循环可以找到前驱节点和区间开始节点
    for (int i = 1; i < m; i++) {
        prev = prev.next;
        start = start.next;
        end = end.next;
    }
    // 第二个for循环可以找到区间结束节点
    for (int i = m; i < n; i++) {
        end = end.next;
    }
    // 找到后继节点
    successor = end.next;
    // 至关重要的一步，将反转区间的最后一个节点和原链表断开，否则会造成死循环
    end.next = null;
    // 将反转后的头节点连在前驱结点后面，这里的 reverseList() 方法直接复用上一题的翻转单链表方法即可
    prev.next = reverseList(start);
    // 反转后，start变成尾结点，把它和后继结点连接起来
    start.next = successor;
    return dummy.next;
}
public ListNode reverseList(ListNode head) {
    ListNode prev = null; 
    ListNode cur = head;
    ListNode temp;
    while (cur != null) {
        temp = cur.next;
        cur.next = prev;
        prev = cur;
        cur = temp;
    }
    return prev;
    }
}
```