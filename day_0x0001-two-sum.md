---
title: "DAY_0X0001: Two Sum"
date: "2023-09-02"
categories: 
  - "algorithm"
  - "leetcode"
tags: 
  - "subject"
  - "typescript"
coverImage: "1b054964a258475bb663f1693a398505.jpg"
---

# Two Sum

- Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
- You may assume that each input would have exactly one solution, and you may not use the same element twice.
- You can return the answer in any order.

# Example 1:

Input: nums = \[2,7,11,15\] target = 9 Output: \[0,1\] Explanation: Because nums\[0\] + nums\[1\] == 9, we return \[0, 1\]

# Example 2:

Input: nums = \[3,2,4\] target = 6 Output: \[1,2\]

# Example 3:

Input: nums = \[3,3\] target = 6 Output: \[0,1\]

# Constraints:

- 2 <= nums.length <= 104
- \-109 <= nums\[i\] <= 109
- \-109 <= target <= 109
- Only one valid answer exists.

# Code

```ts
function twoSum(nums: number[], target: number): number[] {
  const map:Map<number,number> = new Map();
  let result:Array<number> = [];
  nums.forEach((num,index)=>{
    const difference = target - num;
    if(map.has(difference)){
      result = [map.get(difference) as number,index];
    }
    map.set(num,index);
  });
  return result;
};
```

# Principle

- if `A+B=C` then `C - B = A`,`C - A = B`.
- So we only need one loop to directly get the subscript of B or A stored in the map.
