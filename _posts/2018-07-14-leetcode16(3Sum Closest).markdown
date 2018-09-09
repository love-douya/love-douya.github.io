---
layout: post
title:  "3Sum Closest(leetcode16)"
date:   2018-07-14 23:57:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

### Example

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).






### Python solution

```python

import sys

class Solution:
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: ints
        :rtype: int
        """
        result, diff = 0, sys.maxsize
        nums.sort()
        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            left, right = i + 1, len(nums) - 1
            while left < right:
                total = nums[i] + nums[left] + nums[right]
                hold_diff = abs (total - target)
                if not hold_diff:
                    return total     

                if hold_diff  < diff:
                    result = total
                    diff = hold_diff   

                if total < target:
                    left += 1
                
                else:
                    right -= 1                   
        return result

if __name__ == "__main__":
    sys.stdout.write("Input array: \n")
    nums = list(map(int, str(sys.stdin.readline()).strip().split()))
    sys.stdout.write("Input target: \n")
    target = int(str(sys.stdin.readline()).strip())
    sys.stdout.write("Result is: \n" + str(Solution().threeSumClosest(nums, target)))

```