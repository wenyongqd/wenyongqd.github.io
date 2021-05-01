---
title: LeetCode 445
date: 2020-07-04 13:46:29
tags:
    - Linked List

---
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**
> **Input:** (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
  **Output:** 7 -> 8 -> 0 -> 7

![image](https://images.xiaozhuanlan.com/photo/2019/3b0e95a2e5c00ab1071a7232ca329e62.gif)

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<Integer>();
        Stack<Integer> s2 = new Stack<Integer>();
        
        while(l1 != null) {
            s1.push(l1.val);
            l1 = l1.next;
        }
        
        while(l2 != null) {
            s2.push(l2.val);
            l2 = l2.next;
        }
        
        ListNode dummy = new ListNode(0);
        int carry = 0;
        while( !s1.isEmpty() || !s2.isEmpty()) {
            if(!s1.isEmpty()) {
                carry += s1.pop();
            }
            if(!s2.isEmpty()) {
                carry += s2.pop();
            }
            
            ListNode node = new ListNode(carry % 10);
            node.next = dummy.next;
            dummy.next = node;
            
            carry = carry / 10;
            
        }
        if (carry != 0) {
            ListNode node = new ListNode(1);
            node.next = dummy.next;
            dummy.next = node;
        }
        return dummy.next;
            
    }
}
```