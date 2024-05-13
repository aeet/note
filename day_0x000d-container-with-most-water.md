---
title: "DAY_0X000D: Container With Most Water"
date: "2023-09-19"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "152d15ef882b11ebb6edd017c2d2eca2-scaled.jpg"
---

# Container With Most Water

You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height\[i\]).

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

Notice that you may not slant the container.

![](images/question_11.jpg)

Input: height = \[1,8,6,2,5,4,8,3,7\] Output: 49 Explanation: The above vertical lines are represented by array \[1,8,6,2,5,4,8,3,7\]. In this case, the max area of water (blue section) the container can contain is 49.

# Constraints

- n == height.length
- 2 <= n <= 105
- 0 <= height\[i\] <= 104

# Code

```js
var maxArea = function(H) {
    let ans = 0, i = 0, j = H.length-1
    while (i < j) {
        ans = Math.max(ans, Math.min(H[i], H[j]) * (j - i))
        H[i] <= H[j] ? i++ : j--
    }
    return ans
};
```

# Principle

$$$ S = H \* W $$$

- so `↑S` = `↑H` or `↑W`
- We can choose the two elements with the highest and longest width on both sides
