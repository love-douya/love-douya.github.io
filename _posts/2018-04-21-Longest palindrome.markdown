---
layout: post
title:  "Longest palindrome(Leetcode-5)"
date:   2018-04-21 18:20:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode palindrome
---

* content
{:toc}

## Problem

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

### Example 1

>* Input: "babad"
>* Output: "bab"
>* Note: "aba" is also a valid answer.

### Example 2

>* Input: "cbbd"
>* Output: "bb"





### Python solution

```python

#General Way Time complexity O(n^2)
class Solution_General:
    def searchPalindrome(self, s, left, right, startIdx, length):
        step = 1
        while((left - step) >= 0 and (right + step) < len(s)):
            if s[left - step] != s[right + step]:
                break
            step += 1
        wide = right - left + 2 * step - 1
        if length < wide:
            length = wide
            startIdx = left - step + 1
        return s, left, right, startIdx, length

    def longestPalindrome(self, s):
        startIdx = 0
        left = 0 
        right = 0 
        length = 0
        for i in range(0, len(s) - 1):
            if (s[i] == s[i + 1]):
                left = i
                right = i + 1
                s, left, right, startIdx, length = self.searchPalindrome(s, left, right, startIdx, length)
            left = right = i
            s, left, right, startIdx, length = self.searchPalindrome(s, left, right,startIdx, length)
        
        if length == 0:
            length = len(s)
        return s[startIdx : startIdx + length]

#DP Time complexity O(n^2)
class Solution_DP:
    def longestPalindrome(self, s):
        x_axis = y_axis = len(s)
        dp = [[0 for col in range(x_axis)] for row in range(y_axis)]
        left = 0
        right = 0
        length = 0
        for i in range(0, len(s)):
            for j in range(0, i):
                dp[j][i] = (s[i] == s[j] and (i - j < 2 or dp[j + 1][i - 1]))
                if(dp[j][i] and length < i - j + 1):
                    length = i - j + 1
                    left = j
                    right = i
            dp[i][i] = 1
        return s[left : right + 1]

#Manacher's Algorithm Time complexity O(n)
class Solution_Manacher:
    def longestPalindrome(self, s):
        t = '#'.join('^{}$'.format(s)) #填充首尾与分割符使得长度为奇数
        p = [0] * len(t)
        id = 0
        mx = 0
        resId = 0
        resMx = 0
        for i in range(0, len(t), 1):
            if mx > i:
                p[i] = min(p[2 * id - i], mx - i)
            else:
                p[i] = 1
            while t[i + p[i] - 1] == t[i - p[i] - 1]:
                p[i] += 1
            if mx < i + p[i]:
                mx = i + p[i]
                id = i
            if resMx < p[i]:
                resMx = p[i]
                resId = i
        return s[(resId - resMx) // 2 : (resId + resMx) // 2 - 1]

if __name__=="__main__":       
    Solution0 = Solution_General()
    Solution1 = Solution_DP()
    Solution2 = Solution_Manacher()
    print("General Way: " + Solution0.longestPalindrome("adhda"))
    print("DP: " + Solution1.longestPalindrome("adhda"))
    print("Manacher: " + Solution2.longestPalindrome("adhda"))

```