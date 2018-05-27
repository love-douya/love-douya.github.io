---
layout: post
title:  "Median of two sorted arrays(Leetcode-4)"
date:   2018-05-05 18:20:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

### Example 1

> nums1 = [1, 3]
> nums2 = [2]

> The median is 2.0

### Example 2

> nums1 = [1, 2]
> nums2 = [3, 4]

> The median is (2 + 3)/2 = 2.5





### Python solution

```python

class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        list3 = []
        len1 = len(nums1) - 1
        len2 = len(nums2) - 1
        len3 = len1 + len2 + 2
        i = 0
        j = 0
        while i <= len1 and j <= len2:
            if nums1[i] <= nums2[j]:
                list3.append(nums1[i])
                i += 1
            else:
                list3.append(nums2[j])
                j += 1
        while i <= len1:
            list3.append(nums1[i])
            i += 1
        while j <= len2:
            list3.append(nums2[j])
            j += 1
        if len3 % 2 == 0:
            median = (list3[int(len3 / 2 - 1)] + list3[int(len3 / 2)]) / 2
        else:
            median = list3[len3 // 2]
        return median

if __name__ == "__main__":
    nums1 = list(map(int, input("Input Sorted List1: ")))
    nums2 = list(map(int, input("Input Sorted List2: ")))
    print(Solution().findMedianSortedArrays(nums1, nums2))

```