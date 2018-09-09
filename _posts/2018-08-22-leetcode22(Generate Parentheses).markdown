---
layout: post
title:  "Generate Parentheses(leetcode22)"
date:   2018-08-22 19:06:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is: 
```c
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```






### Python solution

```python

import sys

class Solution(object):
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        res = []
        def dfs(res, n, s, left, right) :
            if right == n : res.append(s)
            if left < n :
                dfs(res, n, s + "(", left+1, right)
            if left > right :
                dfs(res, n, s + ")", left, right+1)
        dfs(res, n, '', 0, 0)
        return res

if __name__ == '__main__':
    print('Result is: {0}'.format(Solution().generateParenthesis(int(input('Input number of parentheses pairs: ')))))

```