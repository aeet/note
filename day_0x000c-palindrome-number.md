---
title: "DAY_0X000C: Palindrome Number"
date: "2023-09-17"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "5a828f9ec86a4d2dae9ca5aa67b612cf.jpg"
---

# Palindrome Number

Given an integer x, return true if x is a palindrome, and false otherwise.

# Example 1:

Input: x = 121 Output: true Explanation: 121 reads as 121 from left to right and from right to left.

# Example 2:

Input: x = -121 Output: false Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

# Example 3:

Input: x = 10 Output: false Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

# Code

```js
var isPalindrome = function(x) {
    return Number(x.toString().split('').reverse().join('')) === x;
};
```
