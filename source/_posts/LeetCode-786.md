---
title: LeetCode 786
date: 2020-04-06 10:03:28
tags:
---
```java
class Solution {
    public int[] kthSmallestPrimeFraction(int[] A, int K) {
        double l = 0, r = 1;
        int p = 0, q = 1, cnt = 0;
        int[] ans = new int[]{0, 1};
        while (r - l > 1e-9) {
            double mid = l + (r - l) / 2.0;
            cnt = 0;
            p = 0;
            for(int i = 0, j = 0; i < A.length; i++) {
                while (j < A.length && A[i] > mid * A[j]) j++;
                cnt += A.length - j;
                if (j < A.length && p*A[j] < q*A[i]) {
                    p = A[i];
                    q = A[j];
                }
            }
            if(cnt == K) {
                ans[0] = p;
                ans[1] = q;
                return ans;
            }
            else if (cnt < K) l = mid;
            else r = mid;
        }
        return ans;
    }
}
```