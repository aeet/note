---
title: "DAY_0X000A: Reverse Integer"
date: "2023-09-14"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "b387f7ee883611ebb6edd017c2d2eca2-scaled.jpg"
---

# Reverse Integer

Given a signed 32-bit integer x, return x with its digits reversed. If reversing x causes the value to go outside the signed 32-bit integer range \[-231, 231 - 1\], then return 0.

# Code

```js
var reverse = function (x) {
  let fuhao = true
  if (x > 0) { fuhao = false } else { fuhao = true }
  const arr = Math.abs(x).toString().split("")
  const newArr = [];
  for (let i = arr.length; i > 0; i--) {
    newArr.push(arr[i - 1])
  }
  const j = newArr.join("") * (fuhao ? -1 : 1)
  if (j < Math.pow(-2, 31) || j > Math.pow(2, 31) - 1) { return 0 }
  return j
};
```
