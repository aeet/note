---
title: "DAY_0X0009: Zigzag Conversion"
date: "2023-09-13"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "b9088eb4f72744e1881cb31db18d35a0.jpg"
---

# Zigzag Conversion

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

And then read line by line: "PAHNAPLSIIGYIR"

| P |  | A |  | H |  | N |
| --- | --- | --- | --- | --- | --- | --- |
| A | P | L | S | I | I | G |
| Y |  | I |  | R |  |  |

Write the code that will take a string and make this conversion given a number of rows:

`string convert(string s, int numRows);`

# Example 1

Input: s = "PAYPALISHIRING", numRows = 3 Output: "PAHNAPLSIIGYIR"

# Example 2

Input: s = "PAYPALISHIRING", numRows = 4 Output: "PINALSIGYAHRPI"

# Example 3

Input: s = "A", numRows = 1 Output: "A"

# Constraints

- 1 <= s.length <= 1000
- s consists of English letters (lower-case and upper-case), ',' and '.'.
- 1 <= numRows <= 1000

# Code

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function (s, numRows) {
  if (numRows === 0 || numRows === 1) return s;
  else if (numRows === 2) {
    const s1 = s.split("").filter((v, i) => i % 2 == 0)
    const s2 = s.split("").filter((v, i) => i % 2 != 0)
    return [...s1, ...s2].join("")
  } else {
    let strArr = s.split("")
    let rows = [];
    for (let i = 0; i < numRows; i++) { rows[i] = '' }
    let col = 0;
    let step = -1;
    strArr.forEach((v) => {
      if (col === 0) {
        step = 1;
      } else if (col === numRows - 1) {
        step -= 1;
        col += step;
      }
      rows[col] += v
      col += step;
    })
    return rows.join("");
  }
};
```

# Principle

```
sarr = ['A','B','C','D','E','F','G','H'];
index=[ 0, 1 , 2,  1 , 0 , 1,  2,  1];
rows = 3;
```

| row |  |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| 1 | A |  | E |  |  |
| 2 | B | D | F | H |  |
| 3 | C |  | G |  |  |

- so you can use `step and index` to get item
