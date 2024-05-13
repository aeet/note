---
title: "DAY_0X0012:  3Sum Closest"
date: "2023-09-28"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "a80d2384c6bf40038676260ae705ec94.jpg"
---

# 3Sum Closest

Given an integer array nums of length n and an integer target, find three integers in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

# Example 1

Input: nums = \[-1,2,1,-4\], target = 1 Output: 2 Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

# Example 2

Input: nums = \[0,0,0\], target = 1 Output: 0 Explanation: The sum that is closest to the target is 0. (0 + 0 + 0 = 0).

# Constraints

- 3 <= nums.length <= 500
- \-1000 <= nums\[i\] <= 1000
- \-104 <= target <= 104

# Code

```js
var threeSumClosest = function (nums, target) {
  let result = nums[0] + nums[1] + nums[2];
  nums.sort((a, b) => a - b);
  for (let i = 0; i < nums.length - 2; i++) {
    let j = i + 1;
    let k = nums.length - 1;
    while (j < k) {
      const sum = nums[i] + nums[j] + nums[k];
      if (sum === target) {
        return sum;
      }
      if (sum > target) {
        k--;
      }
      if (sum < target) {
        j++;
      }
      if(Math.abs(sum - target) < Math.abs(result - target)){
        result = sum;
      }
    }
  }
  return result;
};

console.log(threeSumClosest([-1, 2, 1, -4], 1));
```
