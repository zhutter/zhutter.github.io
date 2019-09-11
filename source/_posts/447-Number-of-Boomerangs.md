---
title: 447.Number of Boomerangs
date: 2019-08-09 18:01:01
tags: [Leetcode, easy]
---

# Description

Given *n* points in the plane that are all pairwise distinct, a "boomerang" is a tuple of points `(i, j, k)` such that the distance between `i` and `j` equals the distance between `i`and `k` (**the order of the tuple matters**).

Find the number of boomerangs. You may assume that *n* will be at most **500** and coordinates of points are all in the range **[-10000, 10000]** (inclusive).

**Example:**

```
Input:
[[0,0],[1,0],[2,0]]

Output:
2

Explanation:
The two boomerangs are [[1,0],[0,0],[2,0]] and [[1,0],[2,0],[0,0]]
```

# Solution

```java
public int numberOfBoomerangs(int[][] points) {
        int res = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i=0; i<points.length; i++){
            for(int j=0; j<points.length; j++){
                int d = getDistance(points[i], points[j]);
                map.put(d, map.getOrDefault(d, 0)+1);
            }
            for(int val : map.values()){
                //after capturing the number of points equidistant from i
                //we need to calculate all possible permutaions
                //the number of permutation of size 2 from n is
                //nP2 = n!/(n-2)! = n*(n-1)
                res += val * (val-1);
            }
            map.clear();
        }
        return res;
    }
    private int getDistance(int[] point_a, int[] point_b){
        int x = point_a[0] - point_b[0];
        int y = point_a[1] - point_b[1];
        return x*x + y*y;
    }
```

This solution is provided by [asurana28](https://leetcode.com/asurana28) in discussion area

```
Time complexity:  O(n^2)
Space complexity: O(n)
```

