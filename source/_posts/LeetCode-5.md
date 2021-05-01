---
title: LeetCode 5
date: 2020-03-29 20:07:07
tags:
---
### Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

We define **dp[i][j]** as following:

- **dp[i][j] == ture**, if the substring **Si** ... **Sj** is a palindrome. 
![basecase](https://github.com/azl397985856/leetcode/raw/master/assets/problems/5.longest-palindromic-substring-2.png)

Therefore, the state transition
```java
if (s.charAt(i) == s.charAt(j) && dp[i+1][j-1] == true) {
    dp[i][j] = true;
}
```

**Base case:**
![base](https://github.com/azl397985856/leetcode/raw/master/assets/problems/5.longest-palindromic-substring-3.png)


**Example 1:**

> **Input**: "babad"
  **Output**: "bab"
  **Note**: "aba" is also a valid answer.

**Example 2:**

> **Input**: "cbbd"
  **Output**: "bb"

### Approach: Dynamic Programming

To improve over the brute force solution, we first observe how we can avoid unnecessary re-computation while validating palindromes. Consider the case "ababa". If we already knew that "bab" is a palindrome, it is obvious that "ababa" must be a palindrome since the two left and right end letters are the same.

**解决这类问题的核心思想就是两个字“延伸”，具体来说**

- 如果一个字符串是回文串，那么在它左右分别加上一个相同的字符，那么它一定还是一个回文串
- 如果一个字符串不是回文串，或者在回文串左右分别加不同的字符，得到的一定不是回文串

##### Complexity Analysis

- **Time complexity** : O(n^2) This gives us a runtime complexity of O(n^2)
- **Space complexity** : O(n^2). It uses O(n^2) space to store the table.


### Code

````java
class Solution {
    public String longestPalindrome(String s) {
    
        if (s == null || s.equals("")) return s;
        String ans = "";
        int max = 0;
        boolean[][] dp = new boolean[s.length()][s.length()];
        
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                if (j - i == 0) dp[i][j] = true;
                else if (j - i == 1 && s.charAt(i) == s.charAt(j)) dp[i][j] = true;
                else if (s.charAt(i) == s.charAt(j) && dp[i+1][j-1] == true) dp[i][j] = true;
                
                if (dp[i][j] && j - i + 1 > max) {
                    max = j - i + 1;
                    ans = s.substring(i, j + 1);
                }
            }
        }
        return ans;
    }
}
````