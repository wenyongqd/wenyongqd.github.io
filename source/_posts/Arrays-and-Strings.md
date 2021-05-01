---
title: Arrays and Strings
date: 2020-07-07 17:17:14
tags:
---
### 3 Longest Substring Without Repeating Characters
Given a string, find the length of the longest substring without repeating characters.
**Example 1:**
> **Input:** "abcabcbb"
**Output:** 3 
**Explanation:** The answer is "abc", with the length of 3. 

**Example 2:**

> **Input:** "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

> **Input:** "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int ans = 0;
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0, j = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```

### 8. String to Integer (atoi)

* Implement atoi which converts a string to an integer.
* The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
* The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
* If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
* If no valid conversion could be performed, a zero value is returned.

**Note:**
Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

**Example 1:**
> **Input:** "42"
**Output:** 42

**Example 2:**
> **Input:** "   -42"
**Output:** -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
             
**Example 3:**
> **Input:** "4193 with words"
**Output:** 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.

**Example 4:**
> **Input:** "words and 987"
**Output:** 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
             
**Example 5:**
> **Input:** "-91283472332"
**Output:** -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.

```java
class Solution {
    public int myAtoi(String str) {
             if(str == null){
             return 0;
         }
         
         // 去掉前后空格
         // then check if it is empty, corner case " "
         str = str.trim();
         if(str.length() == 0){
             return 0;
         }
         
         //首个char是符号
         boolean isNeg = false;
         int i = 0;
         if(str.charAt(0) == '+'){
             i++;
         }else if(str.charAt(0) == '-'){
             isNeg = true;
             i++;
         }
         
         int res = 0;
         while(i<str.length() && Character.isDigit(str.charAt(i))){
             char c = str.charAt(i);
             // Overflow
             if(res > Integer.MAX_VALUE/10 || (res == Integer.MAX_VALUE/10 && c>='8')){
                 return isNeg ? Integer.MIN_VALUE : Integer.MAX_VALUE;
             }
             
             res = res*10 + (c-'0');
             i++;
         }
         
         return isNeg ? -res : res;
    }
}
```

### 26. Remove Duplicates from Sorted Array
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

**Example 1:**
>Given nums = [1,1,2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the returned length.

**Example 2:**
>Given nums = [0,0,1,1,1,2,2,3,3,4],
Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.
![image](https://camo.githubusercontent.com/26b1547fb6119bbaec4a110ad27c753415b2b8b2/68747470733a2f2f626c6f672d313235373132363534392e636f732e61702d6775616e677a686f752e6d7971636c6f75642e636f6d2f626c6f672f34793165632e676966)

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) return 0;
        int i = 0;
        for (int j =1; j < nums.length; j++) {
            if (nums[j] != nums[i]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
}
```

### 122. Best Time to Buy and Sell Stock II
Say you have an array prices for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**
>**Input:** [7,1,5,3,6,4]
**Output:** 7
**Explanation:** Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

![image](https://camo.githubusercontent.com/d7d4ad25a184ac051843d7c7099e26cdd25d0ee4/68747470733a2f2f626c6f672d313235373132363534392e636f732e61702d6775616e677a686f752e6d7971636c6f75642e636f6d2f626c6f672f6e6b76646a2e706e67)

```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 1; i < prices.length; i++) {
            if(prices[i] > prices[i-1]) {
                profit = prices[i] - prices[i - 1] + profit;
            }
        }
        return profit;
    }
}
```

### 189. Rotate Array

Given an array, rotate the array to the right by k steps, where k is non-negative.

**Follow up:**

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O(1) extra space?

*Example 1:*

>Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

![image](https://github.com/MisterBooo/LeetCodeAnimation/raw/master/0189-Rotate-Array/Animation/189.gif)

```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (nums.length == 0) return;
        k = k % nums.length;
        
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }
    
    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
}
```

### 387. First Unique Character in a String
Given a string, find the first non-repeating character in it and return its index. If it doesn't exist, return -1.

**Examples:**
>s = "leetcode"
return 0.
s = "loveleetcode"
return 2.

```java
class Solution {
    public int firstUniqChar(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        if (s.length() == 0) return -1;
        if (s.length() == 1) return 0;
        
        for (int i = 0; i < s.length(); i++) {
            if (map.containsKey(s.charAt(i))) {
                map.put(s.charAt(i), 0);
            }else {
                map.put(s.charAt(i), 1);
            }
            
        }
        
        for (int i = 0; i < s.length(); i++) {
            if(map.get(s.charAt(i)) == 1) return i;
        }
        
        return -1;
    }
}
```

### 242. Valid Anagram
Given two strings s and t , write a function to determine if t is an anagram of s.
**Example 1:**

>Input: s = "anagram", t = "nagaram"
Output: true

**Example 2:**

>Input: s = "rat", t = "car"
Output: false

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        char[] s1 = s.toCharArray();
        char[] s2 = t.toCharArray();
        
        Arrays.sort(s1);
        Arrays.sort(s2);
        
        return Arrays.equals(s1, s2);
    }
}
```