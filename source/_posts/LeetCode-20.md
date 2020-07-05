---
title: LeetCode 20
subtitle: "\"Repetition is the mother of all learning.\""

date: 2020-03-27 10:28:09
tags: 
    - LeetCode
---

![practice](https://miro.medium.com/max/1280/1*Rg98i5ViTT24BYAobiNl9Q.png)
<small class="img-hint">“Deliberate practice is not a comfortable activity. It requires sustained effort and concentration. The people who master the art of deliberate practice are committed to being lifelong learners — always exploring and experimenting and refining.” — James Clear</small>

### Approach: Stacks
An interesting property about a valid parenthesis expression is that a sub-expression of a valid expression should also be a valid expression. (Not every sub-expression) e.g.

![approach](https://leetcode.com/problems/valid-parentheses/Figures/20/20-Valid-Parentheses-Recursive-Property.png)

Also, if you look at the above structure carefully, the color coded cells mark the opening and closing pairs of parenthesis. The entire expression is valid, but sub portions of it are also valid in themselves. This lends a sort of a recursive structure to the problem. For e.g. Consider the expression enclosed within the two green parenthesis in the diagram above. The opening bracket at index 1 and the corresponding closing bracket at index 6

> What if whenever we encounter a matching pair of parenthesis in the expression, we simply remove it from the expression?

Let's have a look at this idea below where remove the smaller expressions one at a time from the overall expression and since this is a valid expression, we would be left with an empty string in the end.

> The stack data structure can come in handy here in representing this recursive structure of the problem. We can't really process this from the inside out because we don't have an idea about the overall structure. But, the stack can help us process this recursively i.e. from outside to inwards.

Let us have a look at the algorithm for this problem using stacks as the intermediate data structure.

#### Algorithm - Prefix Sum + Brute force

1. Initialize a stack S.
2. Process each bracket of the expression one at a time.
3. If we encounter an opening bracket, we simply push it onto the stack. This means we will process it later, let us simply move onto the sub-expression ahead.
4. If we encounter a closing bracket, then we check the element on top of the stack. If the element at the top of the stack is an opening bracket of the same type, then we pop it off the stack and continue processing. Else, this implies an invalid expression.
5. In the end, if we are left with a stack still having elements, then this implies an invalid expression.




```java
class Solution {
    public static boolean isValid(String s) {

        Stack stack = new Stack();
        if (s.equals("")) return true;
        stack.push(s.charAt(0));

        for (int i = 1; i < s.length(); i++) {

            if (s.charAt(i) == '(' || s.charAt(i) == '{' || s.charAt(i) == '[') {
                stack.push(s.charAt(i));
            }
            
            else {
                if (stack.isEmpty()) return false;
                if (s.charAt(i) == ')' && !stack.peek().equals('(')) return false;
                if (s.charAt(i) == '}' && !stack.peek().equals('{')) return false;
                if (s.charAt(i) == ']' && !stack.peek().equals('[')) return false;
                stack.pop();
            }
        }
        return stack.isEmpty();
    }
}
```
