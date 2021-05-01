---
title: Tree Questions
date: 2020-07-22 22:16:07
tags:
---

<!-- TOC -->

- [104. Maximum Depth of Binary Tree](#104-maximum-depth-of-binary-tree)
- [98. Validate Binary Search Tree](#98-validate-binary-search-tree)
- [101. Symmetric Tree](#101-symmetric-tree)
- [107. Binary Tree Level Order Traversal II](#107-binary-tree-level-order-traversal-ii)
- [108. Convert Sorted Array to Binary Search Tree](#108-convert-sorted-array-to-binary-search-tree)

<!-- /TOC -->

### 104. Maximum Depth of Binary Tree

Given a binary tree, find its maximum depth.
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
**Note:** A leaf is a node with no children.
**Example:**

Given binary tree [3,9,20,null,null,15,7],

```xml
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

![image](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0104-Maximum-Depth-Of-Binary-Tree/Animation/Animation1.gif)
**Approach 1:** Recursion

> **Intuition** By definition, the maximum depth of a binary tree is the maximum number of steps to reach a leaf node from the root node.

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
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left, right) + 1;
    }
}
```

![image](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0104-Maximum-Depth-Of-Binary-Tree/Animation/Animation2.gif)
**Approach 3:** BFS

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        int count = 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()) {
            int size = queue.size();
            while(size-- >0) {
                TreeNode node = queue.poll();
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            count++;
        }
        return count;
    }
}
```

### 98. Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree (BST).
Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

```xml
    2
   / \
  1   3

**Input:** [2,1,3]
**Output:** true
```

**Example 2:**

```xml
    5
   / \
  1   4
     / \
    3   6

**Input:** [5,1,4,null,null,3,6]
**Output:** false
**Explanation:** The root node's value is 5 but its right child's value is 4.
```

**Approach 1**

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
    public boolean isValidBST(TreeNode root) {
        return isValidBSThelper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean isValidBSThelper(TreeNode root, long min, long max) {
        if (root == null) return true;
        if (root.val >= max || root.val <= min) return false;

        return isValidBSThelper(root.left, min, root.val) && isValidBSThelper(root.right, root.val, max);
    }
}
```

**Approach 2**

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
        TreeNode preNode;
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        if (!isValidBST(root.left)) return false;
        if (preNode != null && preNode.val >= root.val) return false;
        preNode = root;
        if (!isValidBST(root.right)) return false;
        return true;
    }
}
```

### 101. Symmetric Tree

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

```xml
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following [1,2,2,null,3,null,3] is not:

```xml
    1
   / \
  2   2
   \   \
   3    3
```

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
    public boolean isSymmetric(TreeNode root) {
        return isMirror(root, root);
    }

    public boolean isMirror(TreeNode r1, TreeNode r2) {
        if (r1 == null && r2 == null) return true;
        if (r1 == null || r2 == null) return false;
        if (r1.val != r2.val) return false;
        return isMirror(r1.left, r2.right) && isMirror(r1.right, r2.left);
    }
}
```

### 107. Binary Tree Level Order Traversal II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],

```xml
    3
   / \
  9  20
    /  \
   15   7
```

return its bottom-up level order traversal as:

```xml
[
  [15,7],
  [9,20],
  [3]
]
```

```java
public List<List<Integer>> levelOrderBottom(TreeNode root) {

    List<List<Integer>> result = new ArrayList<List<Integer>>();
    if(root==null) return result;
    Queue<TreeNode> q = new LinkedList<>();
    q.add(root);
    while(q.size()>0){
        List<Integer> list = new ArrayList<>();
        int size = q.size();
        for(int i=0; i<size; i++){
            TreeNode node = q.poll();
            list.add(node.val);
            if(node.left!=null) q.add(node.left);
            if(node.right!=null) q.add(node.right);
        }
        result.add(0,list);
    }
    return result;

}
```

### 108. Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

**Example:**

Given the sorted array: [-10,-3,0,5,9],

```XML
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

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
    public TreeNode sortedArrayToBST(int[] nums) {
        return dfs(nums, 0, nums.length - 1);
    }

    public TreeNode dfs(int[] nums, int lo, int hi) {
        if (lo > hi) return null;
        int mid = lo + (hi - lo)/2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = dfs(nums, lo, mid - 1);
        root.right = dfs(nums, mid + 1, hi);
        return root;
    }
}
```
