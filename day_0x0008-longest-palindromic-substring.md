---
title: "DAY_0X0008: Longest Palindromic Substring"
date: "2023-09-11"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "subject"
  - "typescript"
coverImage: "35cb18d38a894c3fba042d2d19d6afd3.jpg"
---

# Longest Palindromic Substring

Given a string s, return the longest palindromic substring in s.

# Example 1

Input: s = "babad" Output: "bab" Explanation: "aba" is also a valid answer.

# Example 2

Input: s = "cbbd" Output: "bb"

# Constraints

- 1 <= s.length <= 1000
- s consist of only digits and English letters.

# Code

```ts
function longestPalindrome(s: string): string {
  if (!s || s.length <= 1) { return s }
  let longestPalindrome = s.substring(0, 1)
  for (let i = 0; i < s.length; i++) {
    [expand(s, i, i), expand(s, i, i + 1)].forEach((maybeLongest) => {
      if (maybeLongest.length > longestPalindrome.length) {
        longestPalindrome = maybeLongest
      }
    })
  }
  return longestPalindrome
}

function expand(s: string, begin: number, end: number): string {
  while (begin >= 0 && end <= s.length - 1 && s[begin] === s[end]) {
    begin--
    end++
  }
  return s.substring(begin + 1, end)
}
```

# Principle

- Use the first character of the string as starting value.
- The expand function expands from the current character position to both ends of the entire string through the begin and end positions, and records the indexes of the left and right ends of the palindrome.
- `expand(s, i, i)`, `expand(s, i, i + 1)` corresponding to the situations of `aba`,`aabb`
