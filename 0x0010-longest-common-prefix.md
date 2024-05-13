---
title: "DAY_0X0010: Longest Common Prefix"
date: "2023-09-27"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "10ea0cd6882111ebb6edd017c2d2eca2-scaled.jpg"
---

# Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

# Example 1

Input: strs = \["flower","flow","flight"\] Output: "fl"

# Example 2

Input: strs = \["dog","racecar","car"\] Output: "" Explanation: There is no common prefix among the input strings.

# Constraints

- 1 <= strs.length <= 200
- 0 <= strs\[i\].length <= 200
- strs\[i\] consists of only lowercase English letters.

# code

```js
var longestCommonPrefix = function (strs) {
  strs = strs.sort((a, b) => b.length - a.length);
  let result = "";
  const template = strs.shift();
  for (let i = 0; i < template.length; i++) {
    const char = template[i];
    if (strs.every((str) => str[i] === char)) {
      result += char;
    } else {
      break;
    }
  }
  return result;
};
```
