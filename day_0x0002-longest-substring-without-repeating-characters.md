---
title: "DAY_0X0002: Longest Substring Without Repeating Characters"
date: "2023-09-03"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "subject"
  - "typescript"
coverImage: "742214a6beab4aed9c4df8f79f3084d2-scaled.jpg"
---

# Longest Substring Without Repeating Characters

Given a string s, find the length of the longest substring without repeating characters.

# Example 1:

Input: s = "abcabcbb" Output: 3 Explanation: The answer is "abc", with the length of 3.

# Example 2:

Input: s = "bbbbb" Output: 1 Explanation: The answer is "b", with the length of 1.

# Example 3:

Input: s = "pwwkew" Output: 3 Explanation: The answer is "wke", with the length of 3. Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

# Constraints:

- 0 <= s.length <= 5 \* 104 s
- consists of English letters, digits, symbols and spaces.

# Code

```ts
function lengthOfLongestSubstring(s: string): number {
  let max = 0;
  let str = "";
  for (let i = 0; i < s.length; i++) {
    const index = str.indexOf(s[i]);
    if (index !== -1) {
      str = str.substr(index + 1);
    }
    str += s[i];
    max = Math.max(max, str.length);
  }
  return max;
}
```

# Principle

```
// i = 0; index = -1; str = 'a'; max = 1
// i = 1; index = -1; str = 'ab'; max = 2
// i = 2; index = -1; str = 'abc'; max = 3
// i = 3; index = 0; str = 'b'; max = 3
// i = 4; index = 1; str = 'c'; max = 3
// i = 5; index = 2; str = 'abc'; max = 3
// i = 6; index = 0; str = 'b'; max = 3
// i = 7; index = 1; str = 'c'; max = 3
```
