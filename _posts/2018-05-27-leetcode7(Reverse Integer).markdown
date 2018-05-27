---
layout: post
title:  "Reverse Integer(Leetcode-7)"
date:   2018-05-27 18:31:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Given a 32-bit signed integer, reverse digits of an integer.

### Example 1

>* Input: 123
>* Output: 321

### Example 2

>* Input: -123
>* Output: -321

### Example 3

>* Input: 120
>* Output: 21





### Python solution

```python

import ctypes

class Solution:
    def reverse(self, x):
        rev = 0
        while(x != 0):
            if(x < 0):
                rev = rev * 10 - abs(x) % 10
            else:
                rev = rev * 10 + x % 10
            if ((rev < -(2**31)) or (rev > (2**31)-1)):
                return 0
            x = int(float(x) / 10)
        return rev

if __name__ == "__main__":
    raw_number = int(input("Input number: "))
    modified_number = ctypes.c_long(raw_number & 0xFFFFFFFF).value
    print(Solution().reverse(modified_number))

```