---
title: "DAY_0X0003: Valid Parentheses"
date: "2023-09-04"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "6fabe2bad60e4d6eb0e8a4ef804569e5.png"
---

# Valid Parentheses

Given a string s containing just the characters `{,},(,),[,]` determine if the input string is valid. An input string is valid if: Open brackets must be closed by the same type of brackets. Open brackets must be closed in the correct order. Every close bracket has a corresponding open bracket of the same type.

# Example 1:

Input: s = () Output: true

# Example 2:

Input: s = ()\[\]{} Output: true

# Example 3:

Input: s = (\] Output: false

# Constraints:

- 1 <= s.length <= 104 s
- consists of parentheses only `()[]{}`

# Code

```js
function isValid(s) {
  const replacedStr = s.replace(/[^\[\](){}]+/g);
  const strArry = replacedStr.split();
  const validArr = [];
  while (strArry.length) {
    if (validArr.length > 0) {
      const a = strArry.pop();
      const e = validArr.pop();
      if (!equal(a, e)) {
        validArr.push(e);
        validArr.push(a);
      }
    } else {
      validArr.push(strArry.pop());
    }
  }
  if (strArry.length === 0 && validArr.length === 0) {
    return true;
  } else {
    return false;
  }
}

function equal(a, b) {
  if (a === "[" && b === "]") {
    return true;
  } else if (a === "(" && b === ")") {
    return true;
  } else if (a === "{" && b === "}") {
    return true;
  }
  return false;
}
```

# Principle

- Two arrays, take out a character from the first one. If there is an element in the second array at this time, then take out the tail element in the second array to determine whether it is equal. If it is equal, eliminate it. If it is not equal, put it back to the end of the queue. , and then put the elements taken out from the first array to the end of the second array.
- Finally, determine whether the two arrays are empty. If they are empty at the same time, it will be deemed that all characters have been eliminated.
