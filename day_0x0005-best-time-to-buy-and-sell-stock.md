---
title: "DAY_0x0005: Best Time to Buy and Sell Stock"
date: "2023-09-06"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "bb4620514a96428581406ad83c3aa1c7.jpg"
---

# Best Time to Buy and Sell Stock

You are given an array prices where prices\[i\] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

# Example 1:

Input: prices = \[7,1,5,3,6,4\] Output: 5 Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5. Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

# Example 2:

Input: prices = \[7,6,4,3,1\] Output: 0 Explanation: In this case, no transactions are done and the max profit = 0.

# Constraints:

1 <= prices.length <= 105 0 <= prices\[i\] <= 104

# Code

```js
const price1 = [0, 7, 1, 5, 3, 6, 4]
const price2 = [7, 6, 4, 3, 1]
const price3 = [7, 6, 4, 4, 2, 3]
const price4 = [7, 6, 4, 4, 1, 2, 3, 1]
const price5 = [7, 2, 4, 6, 7, 2, 7, 1]

function maxProfit(prices) {
  let value = 0;
  let leftPtr = 0;
  let rightPtr = 1;
  while (rightPtr < prices.length) {
    if (prices[rightPtr] > prices[leftPtr]) {
      const diff = prices[rightPtr] - prices[leftPtr]
      if (diff > value) { value = diff }
    } else {
      leftPtr = rightPtr;
    }
    rightPtr++;
  }
  return value;
};

console.log(maxProfit(price1))
console.log(maxProfit(price2))
console.log(maxProfit(price3))
console.log(maxProfit(price4))
console.log(maxProfit(price5))
```

# principle

```
const price1 = [0, 7, 1, 5, 3, 6, 4]

step1: [0, 7, 1, 5, 3, 6, 4]
        l  r
        r - l = 7;  max=7; r++;

step2: [0, 7, 1, 5, 3, 6, 4]
        l     r
        l = r; r++;
       [0, 7, 1, 5, 3, 6, 4]

step3: [0, 7, 1, 5, 3, 6, 4]
              l  r
        r - l = 4; max=7; r++;

step4: [0, 7, 1, 5, 3, 6, 4]
              l     r
        r - l = 2; max=2; r++;
```
