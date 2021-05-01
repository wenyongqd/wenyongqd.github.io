---
title: Collections of Binatry Tree
date: 2020-07-06 11:28:59
tags:
    - Binary Tree
---

> The basic idea of binary tree algorithm design: Defining the manipulation in the current node and the last things are thrown to the framework.


```java
void traverse(TreeNode root) {
    // The manipulation required in the root node should be written here.
    // Other things will be resolved by the framework.
    traverse(root.left);
    traverse(root.right);
}

```

### 100. Same Tree
Given two binary trees, write a function to check if they are the same or not.
Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Example:**
```shell script
Input:     1         1
          / \       / \
         2   3     2   3

        [1,2,3],   [1,2,3]

Output: true
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
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (q == null && p == null) return true;
        if (q == null || p == null) return false;
        if (q.val != p.val) return false;
        return isSameTree(q.left, p.left) && isSameTree(q.right, p.right);
    }
}
```

### 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

**example**, this binary tree [1,2,2,3,4,4,3] is symmetric:
```html
    1
   / \
  2   2
 / \ / \
3  4 4  3
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

### 104. Maximum Depth of Binatry Tree
Given a binary tree, find its maximum depth.
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
**Note:** A leaf is a node with no children.
**Example:**
Given binary tree [3,9,20,null,null,15,7],
```shell script
    3
   / \
  9  20
    /  \
   15   7
```
return its depth = 3.

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
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

### 102. Binary Tree Level Order Traversal
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
```shell script
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:
> [
    [3],
    [9,20],
    [15,7]
  ]

![image](https://images.xiaozhuanlan.com/photo/2019/2338ef7f68e1c09dacef7b67d943a0a9.gif)
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
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> levels = new ArrayList<List<Integer>>();
        if (root == null) return levels;
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.add(root);
        int level = 0;
        while (!queue.isEmpty()) {
            levels.add(new ArrayList<Integer>());
            int level_length = queue.size();
            for (int i = 0; i < level_length; i++) {
                TreeNode node = queue.remove();
                levels.get(level).add(node.val);
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            }
            level++;
        }
        return levels;
    }
}
```

### 814. Binary Tree Pruning
We are given the head node root of a binary tree, where additionally every node's value is either a 0 or a 1.
Return the same tree where every subtree (of the given tree) not containing a 1 has been removed.
(Recall that the subtree of a node X is X, plus every node that is a descendant of X.)
> **Example 1**:
  **Input:** [1,null,0,0,1]
  **Output:** [1,null,0,null,1]
   
> **Explanation:** 
  Only the red nodes satisfy the property "every subtree not containing a 1".
  The diagram on the right represents the answer.

![image](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/04/06/1028_2.png)

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
    public TreeNode pruneTree(TreeNode root) {
        return containsOne(root) ? root : null;
    }

    public boolean containsOne(TreeNode node) {
        if (node == null) return false;
        boolean left = containsOne(node.left);
        boolean right = containsOne(node.right);
        if (!left) node.left = null;
        if (!right) node.right = null;
        return node.val == 1 || left || right;
    }
}
```
```java
class Solution {
    public TreeNode pruneTree(TreeNode root) {
    if (root == null) return root;
    root.left = pruneTree(root.left);
    root.right = pruneTree(root.right);
    return (root.val == 1 || root.left != null || root.right != null) ? root : null;
    }
}
```

### 669. Trim a Binary Search Tree
Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in [L, R] (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

**Example 1:**

```shell script
Input: 
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3

Output: 
      3
     / 
   2   
  /
 1
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
    public TreeNode trimBST(TreeNode root, int L, int R) {
        if (root == null) return root;
        if (root.val < L) return trimBST(root.right, L, R);
        if (root.val > R) return trimBST(root.left, L, R);
        
        root.left = trimBST(root.left, L, R);
        root.right = trimBST(root.right, L, R);
        
        return root;
    }
}
```

### 1325. Delete Leaves With a Given Value
Given a binary tree root and an integer target, delete all the leaf nodes with value target.

Note that once you delete a leaf node with value target, if it's parent node becomes a leaf node and has the value target, it should also be deleted (you need to continue doing that until you can't).

**Example:**
![image](https://assets.leetcode.com/uploads/2020/01/09/sample_1_1684.png)

> Input: root = [1,2,3,2,null,2,4], target = 2
  Output: [1,null,3,null,4]
  Explanation: Leaf nodes in green with value (target = 2) are removed (Picture in left). 
  After removing, new nodes become leaf nodes with value (target = 2) (Picture in center).

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
    public TreeNode removeLeafNodes(TreeNode root, int target) {
        if (root == null) return null;
        root.left = removeLeafNodes(root.left, target);
        root.right = removeLeafNodes(root.right, target);
        return root.left != null || root.right != null || root.val != target ? root : null;
    }
}
```

### 112. Path Sum
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

**Note:** A leaf is a node with no children.

**Example:**
Given the below binary tree and sum = 22,
```shell script
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
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
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) return false;
        sum -= root.val;
        if (root.left == null && root.right == null) return sum == 0;
        return hasPathSum(root.left, sum) || hasPathSum(root.right, sum);
    }
}
```

### 113. Path Sum II
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
**Note:** A leaf is a node with no children.
**Example:**
Given the below binary tree and sum = 22,
```shell script
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
```
**Return:**
> [
     [5,4,11,2],
     [5,8,4,5]
  ]

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
        private void recurseTree(TreeNode node, int remainingSum, List<Integer> pathNodes, List<List<Integer>> pathsList) {
        
        if (node == null) return;
        pathNodes.add(node.val);
        if (remainingSum == node.val && node.left == null && node.right == null) {
            pathsList.add(new ArrayList<>(pathNodes));
        } else {
            recurseTree(node.left, remainingSum - node.val,pathNodes, pathsList);
            recurseTree(node.right, remainingSum - node.val,pathNodes, pathsList);
        }

        pathNodes.remove(pathNodes.size() - 1);
    }
    
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> pathsList = new ArrayList<List<Integer>>();
        List<Integer> pathNodes = new ArrayList<Integer>();
        recurseTree(root, sum, pathNodes, pathsList);
        return pathsList;        
    }
}
```
Reference: [https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban]