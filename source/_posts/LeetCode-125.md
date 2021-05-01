---
title: LeetCode 125
date: 2020-03-30 08:54:14
tags:
---
### Approach: Two Pointer

**Intuition**

If you take any ordinary string, and concatenate its reverse to it, you'll get a palindrome. This leads to an interesting insight about the converse: every palindrome half is reverse of the other half.

Simply speaking, if one were to start in the middle of a palindrome, and traverse outwards, they'd encounter the same characters, in the exact same order, in both halves!

##### Algorithm

Since the input string contains characters that we need to ignore in our palindromic check, it becomes tedious to figure out the real middle point of our palindromic input.
> Instead of going outwards from the middle, we could just go inwards towards the middle!

So, if we start traversing inwards, from both ends of the input string, we can expect to see the same characters, in the same order.

The resulting algorithm is simple:

- Set two pointers, one at each end of the input string
- If the input is palindromic, both the pointers should point to equivalent characters, at all times.
    - If this condition is not met at any point of time, we break and return early.
- We can simply ignore non-alphanumeric characters by continuing to traverse further.
Continue traversing inwards until the pointers meet in the middle.

**思路**

这是一道考察回文的题目，而且是最简单的形式，即判断一个字符串是否是回文。

针对这个问题，我们可以使用头尾双指针:

- 如果两个指针的元素不相同，则直接返回false,
- 如果两个指针的元素相同，我们同时更新头尾指针，循环。 直到头尾指针相遇。

拿“noon”这样一个回文串来说，我们的判断过程是这样的：
![image](https://github.com/azl397985856/leetcode/raw/master/assets/problems/125.valid-palindrome-1.png)

拿“abaa”这样一个不是回文的字符串来说，我们的判断过程是这样的
![image2](https://github.com/azl397985856/leetcode/raw/master/assets/problems/125.valid-palindrome-2.png)

```java
class Solution {
    public boolean isPalindrome(String s) {
        
        for(int i = 0, j = s.length() - 1; i < j; i++, j--) {
            while (i < j && !Character.isLetterOrDigit(s.charAt(i))) i++;
            while (i < j && !Character.isLetterOrDigit(s.charAt(j))) j--;
            if (i < j && Character.toLowerCase(s.charAt(i)) != Character.toLowerCase(s.charAt(j))) return false;
        }
        return true;
    }
}
```

#### **Complexity Analysis**

**Time complexity** : O(n), in length nn of the string. We traverse over each character at-most once, until the two pointers meet in the middle, or when we break and return early.

**Space complexity** : O(1). No extra space required, at all.