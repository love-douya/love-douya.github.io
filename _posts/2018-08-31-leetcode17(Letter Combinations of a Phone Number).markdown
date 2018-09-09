---
layout: post
title:  "Letter Combinations of a Phone Number(Leetcode17)"
date:   2018-08-31 19:06:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![leetcode17 picture](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/leetcode17%20picture.png)

### Example

>* Input: "23"
>* Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].





### Python solution

```python

class Solution1:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        dic = {'0': [' '], '1': [''], '2': ['a', 'b', 'c'], '3': ['d', 'e', 'f'],
               '4': ['g', 'h', 'i'], '5': ['j', 'k', 'l'],
               '6': ['m', 'n', 'o'], '7': ['p', 'q', 'r', 's'],
               '8': ['t', 'u', 'v'], '9': ['w', 'x', 'y', 'z']}
    
        result = ['']
        if not digits:
            return []
        else:
            for i in digits:
                result = [k + j for j in dic[i] for k in result]
            return result

class Solution2:
    def letterCombinations(self, digits):
        dict_num = { '1': '', '2': 'abc', '3': 'def',
        '4': 'ghi', '5': 'jkl', '6': 'mno',
        '7': 'pqrs','8': 'tuv', '9': 'wxyz',
        '0': ' '}
        if not digits:
            return []
        else:
            answer = ['']
            for i in digits:
                answer = [b+a for a in dict_num[i] for b in answer] 
            return answer

if __name__ == '__main__':
    print(Solution1().letterCombinations(input('Input the phone number: ')))

```