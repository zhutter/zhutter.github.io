---
title: 435. Minimum Moves to Equal Array Elements
date: 2019-09-11 20:00:37
tags: [leetcode, easy]
---

# 435. Minimum Moves to Equal Array Elements

## Sample code

```java
int min = nums[0];
int sum = nums[0];
for(int i=1; i<nums.length; i++){
  if(nums[i] < min){
    min = nums[i];
  }
  sum += nums[i];
}
return sum - min*n;
```

One good explanation in discuss area:

> `sum + move*(n-1)  = x*n`
>
> `x = min + move`

`x = min + move` may be a liitle confusing, it comes from two observations:

1. The minimum number will always be minium until it reaches the goal number, because other numbers(except the max)  increased too.
2. So if the final number is `x`, then `x = min + move` 