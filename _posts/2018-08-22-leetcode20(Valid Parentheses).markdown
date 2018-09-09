---
layout: post
title:  "Valid Parentheses(leetcode20)"
date:   2018-08-22 19:06:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- [x] Open brackets must be closed by the same type of brackets.
- [x] Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

### Example 1

>* Input: "()"
>* Output: true

### Example 2

>* Input: "()[]{}"
>* Output: true

### Example 3

>* Input: "(]"
>* Output: false

### Example 4

>* Input: "([)]"
>* Output: false

### Example 5
>* Input: "{[]}"
>* Output: true




### Python solution

```python

class Solution(object):
    def isValid(self, s):
        input_list = list(s)
        stack = []
        while input_list:
            a = input_list.pop()
            if a == ')' or a == ']' or a == '}':
                stack.append(a)
            else:
                if stack:
                    b = stack.pop()
                    if not self.isMatch(a, b):
                        return False
                else:
                    return False       

        if stack:
            return False
        else:
            return True

    def isMatch(self, key, value):
        dic = { '(' : ')' , '[' : ']' , '{' : '}' }
        if dic[key] != value:
            return False
        else:
            return True

if __name__ == '__main__':
    print(Solution().isValid(input('Input String: ')))

```