---
title: Binary Tree Traversal
subtitle: "\"一切过往, 皆为序章 \", \"直挂云帆, 乘风破浪 \""
date: 2020-07-05 13:58:59
header-img: "the-caucasus-5299607_1280.webp"
tags:

---

## Preorder Iterative
![image](IMG_4488BB402A93-1.jpeg)

#### 144. Binary Tree Preorder Traversal
Given a binary tree, return the preorder traversal of its nodes' values.

**Example:**

> **Input:** [1,null,2,3]
     1
      \
       2
      /
     3
  **Output:** [1,2,3]

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) return res;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        
        while(!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            res.add(cur.val);
            if (cur.right != null) {
                stack.push(cur.right);
            }
            if (cur.left != null) {
                stack.push(cur.left);
            }
        }
        return res;
    }
}
```



## Inorder Iterative
![image](IMG_E7E1EDE871D5-1.jpeg)

#### 94. Binary Tree Inorder Traversal 

Given a binary tree, return the inorder traversal of its nodes' values.

**Example:**
> **Input:** [1,null,2,3]
     1
      \
       2
      /
     3
  **Output:** [1,3,2]

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        Deque<TreeNode> stack = new ArrayDeque<>();
        while (!stack.isEmpty() || root != null) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            
            root = stack.pop();
            res.add(root.val);
            
            root = root.right;
        }
        return res;
    }
}
```
## Postorder Iterative

![image](IMG_EB6D2AAD8D60-1.jpeg)

**Preorder VS Postorder**

![image](IMG_A8823501F462-1.jpeg)

#### 145. Binary Tree Postorder Traversal <font color=red><Hard\></font>
Given a binary tree, return the postorder traversal of its nodes' values.

**Example:**

> **Input:** [1,null,2,3]
     1
      \
       2
      /
     3
  **Output:** [3,2,1]

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();
        if (root == null) return res;
        Deque<TreeNode> stack = new ArrayDeque<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            res.addFirst(cur.val);
            
            if (cur.left != null) {
                stack.push(cur.left);
            }
            if (cur.right != null) {
                stack.push(cur.right);
            }
        }
        return res;
    }
}
```