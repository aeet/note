---
title: "DAY_0x0007: Pascal's Triangle"
date: "2023-09-10"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "fc88ae3bfbd54d2785584fee1f7eb70f.jpg"
---

# Pascal's Triangle

Given an integer numRows, return the first numRows of Pascal's triangle.

In Pascal's triangle, each number is the sum of the two numbers directly above it as shown:

![](images/PascalTriangleAnimated2.gif)

# Example 1

Input: numRows = 5 Output: \[\[1\],\[1,1\],\[1,2,1\],\[1,3,3,1\],\[1,4,6,4,1\]\]

# Example 2

Input: numRows = 1 Output: \[\[1\]\]

# Constraints

1 <= numRows <= 30

# Code

```js
/**
 * @param {number} numRows
 * @return {number[][]}
 */
var generate = function(numRows) {
    let triangle = [];
    if (numRows === 0) return triangle;

    triangle.push([1]);

    for (let i = 1; i < numRows; i++) {
        let prevRow = triangle[i - 1];
        let newRow = [1];

        for (let j = 1; j < prevRow.length; j++) {
            newRow.push(prevRow[j - 1] + prevRow[j]);
        }

        newRow.push(1);
        triangle.push(newRow);
    }

    return triangle;
};
```
