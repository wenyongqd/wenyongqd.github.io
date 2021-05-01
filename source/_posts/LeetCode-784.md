---
title: LeetCode 784
date: 2020-04-20 10:30:54
tags:
---
```java
class Solution {
  public List<String> letterCasePermutation(String S) {
    List<String> ans = new ArrayList<>();
    dfs(S.toCharArray(), 0, ans);
    return ans;
  }
  
  private void dfs(char[] S, int i, List<String> ans) {
    if (i == S.length) {
      ans.add(new String(S));
      return;
    }    
    dfs(S, i + 1, ans);    
    if (!Character.isLetter(S[i])) return;
    S[i] ^= 1 << 5;
    dfs(S, i + 1, ans);
    S[i] ^= 1 << 5;
  }
}
```