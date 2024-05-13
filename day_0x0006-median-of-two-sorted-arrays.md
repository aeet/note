---
title: "DAY_0x0006: Median of Two Sorted Arrays"
date: "2023-09-07"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "javascript"
  - "subject"
coverImage: "2336f3f9f65d49ebb452ace245501337.jpg"
---

# Median of Two Sorted Arrays

Given two sorted arrays nums1 and nums2 of size m and n respectively, return the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

# Example 1:

Input: nums1 = \[1,3\], nums2 = \[2\] Output: 2.00000 Explanation: merged array = \[1,2,3\] and median is 2.

# Example 2:

Input: nums1 = \[1,2\], nums2 = \[3,4\] Output: 2.50000 Explanation: merged array = \[1,2,3,4\] and median is (2 + 3) / 2 = 2.5.

# Constraints:

- nums1.length == m
- nums2.length == n
- 0 <= m <= 1000
- 0 <= n <= 1000
- 1 <= m + n <= 2000
- \-106 <= nums1\[i\], nums2\[i\] <= 106

# Code

```js
var findMedianSortedArrays = function (nums1, nums2) {
  const nums3 = [...nums1, ...nums2]
  const nums4 = nums3.sort((a, b) => a - b)
  if (nums4.length % 2 === 1) {
    return nums4[Math.floor(nums4.length / 2)]
  } else {
    return (nums4[Math.floor(nums4.length / 2) - 1] + nums4[Math.floor(nums4.length / 2)]) / 2
  }
};
```
