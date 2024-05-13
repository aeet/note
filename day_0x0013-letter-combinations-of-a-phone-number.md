---
title: "DAY_0X0013: Letter Combinations of a Phone Number"
date: "2023-10-21"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "2ed7cfb8882411ebb6edd017c2d2eca2.png"
---

# Letter Combinations of a Phone Number

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![undefined](images/1200px-telephone-keypad2svg.png)

Example 1:

Input: digits = "23" Output: \["ad","ae","af","bd","be","bf","cd","ce","cf"\] Example 2:

Input: digits = "" Output: \[\] Example 3:

Input: digits = "2" Output: \["a","b","c"\]

Constraints:

0 <= digits.length <= 4 digits\[i\] is a digit in the range \['2', '9'\].

# Code

```js
/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function (digits) {
  let result = [];
  if (!digits) return result;

  const mapping = [
    "",
    "",
    "abc",
    "def",
    "ghi",
    "jkl",
    "mno",
    "pqrs",
    "tuv",
    "wxyz",
  ];
  result = mapping[digits[0]].split("");
  digits = digits.slice(1);
  result = asdf(result, digits, mapping);
  return result;
};

function asdf(result, digits, mapping) {
  if (digits.length === 0) return result;
  const newResult = [];
  for (let i = 0; i < result.length; i++) {
    for (let j = 0; j < mapping[digits[0]].length; j++) {
      newResult.push(result[i] + mapping[digits[0]][j]);
    }
  }
  return asdf(newResult, digits.slice(1), mapping);
}

console.log(letterCombinations("235"))
```
