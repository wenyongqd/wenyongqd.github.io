---
title: LeetCode 399
date: 2020-04-13 13:05:49
tags:
---
```java
class Solution {
    Map<String, HashMap<String, Double>> g =new HashMap<>();
    public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
        
        int index = 0;
        for( List<String> equation : equations) {
            String a = equation.get(0);
            String b = equation.get(1);
            double k = values[index];
            g.computeIfAbsent(a, l -> new HashMap<String, Double>()).put(b, k);
            g.computeIfAbsent(b, l -> new HashMap<String, Double>()).put(a, 1.0/k);
            index++;
        }
        
        double[] ans = new double[queries.size()];
        int i = 0;
        for (List<String> query : queries) {
            String a = query.get(0);
            String b = query.get(1);
            if (!g.containsKey(a) || !g.containsKey(b)) {
                ans[i] = -1.0;
            } else {        
                ans[i] = dfs(a, b, new HashSet<String>());
            }
            i++;
        }
        return ans;
    }
    
    private double dfs(String x, String y, Set<String> visited) {
        if (x.equals(y)) return 1.0;
        visited.add(x);
        if (!g.containsKey(x)) return -1.0;
        for (String n : g.get(x).keySet()) {
            if (visited.contains(n)) continue;
            visited.add(n);
            double d = dfs(n, y, visited);
            if (d > 0) return d * g.get(x).get(n);
        }
        return -1.0;
  }
}
```