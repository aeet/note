---
title: "DAY_0x0004: Add Two Numbers"
date: "2023-09-05"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "f1a63f1914394ad2a57bfedb0a93e4bf.jpg"
---

# Add Two Numbers

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

# Example 1

Input: l1 = \[2,4,3\], l2 = \[5,6,4\] Output: \[7,0,8\] Explanation: 342 + 465 = 807.

# Example 2

Input: l1 = \[0\], l2 = \[0\] Output: \[0\]

# Example 3

Input: l1 = \[9,9,9,9,9,9,9\], l2 = \[9,9,9,9\] Output: \[8,9,9,9,0,0,0,1\]

# Constraints

- The number of nodes in each linked list is in the range \[1, 100\].
- 0 <= Node.val <= 9
- It is guaranteed that the list represents a number that does not have leading zeros.

# Code

```js
function ListNode(next, val) {
  this.val = val === undefined ? 0 : val;
  this.next = next === undefined ? null : next;
}

var addTwoNumbers = function (l1, l2) {
    let l1Arr = [];
    let l2Arr = [];
    while (l1) {
        l1Arr.push(l1.val);
        l1 = l1.next;
    }
    while (l2) {
        l2Arr.push(l2.val);
        l2 = l2.next;
    }
    let l1Num = BigInt(l1Arr.reverse().join(""));
    let l2Num = BigInt(l2Arr.reverse().join(""));
    let sum = l1Num + l2Num;
    let sumArr = sum.toString().split("");
    let sumList = new ListNode(null, sumArr[0]);
    for (let i = 1; i < sumArr.length; i++) {
        sumList = new ListNode(sumList, sumArr[i]);
    }
    return sumList;
};
```
