---
title: LeetCode 79. word search
date: 2020-04-22 11:56:23
tags:
---

new
```java
class Solution {
    public boolean exist(char[][] board, String word) {
        for(int r = 0; r < board.length; r++) {
            for (int c = 0; c < board[0].length; c++) {
                if (board[r][c] == word.charAt(0)) {
                    if (helper(board, word, r, c, 0))
                        return true;
                }
            }
        }
        return false;
    }
    
    public boolean helper(char[][] board, String word, int r, int c, int start) {
        if (start == word.length()) return true;
        if (!isvalid(board, r, c) || board[r][c] != word.charAt(start)) return false;
        
        board[r][c] = '*';
        boolean res = helper(board, word, r + 1, c, start + 1)
            || helper(board, word, r, c + 1, start + 1)
            || helper(board, word, r - 1, c, start + 1)
            || helper(board, word, r, c - 1, start + 1);
        board[r][c] = word.charAt(start);
        return res;          
    }

    public boolean isvalid(char[][] board, int r, int c) {
        return r >= 0 && r < board.length && c >= 0 && c < board[0].length;
    }
}
```