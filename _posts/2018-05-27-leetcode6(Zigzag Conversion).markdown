---
layout: post
title:  "Zigzag Conversion(Leetcode-6)"
date:   2018-05-15 18:40:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

> P   A   H   N

> A P L S I I G

> Y   I   R

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

> string convert(string s, int numRows);

### Example 1

>* Input: s = "PAYPALISHIRING", numRows = 3
>* Output: "PAHNAPLSIIGYIR"

### Example 2

>* Input: s = "PAYPALISHIRING", numRows = 4
>* Output: "PINALSIGYAHRPI"
>* Explanation:

> P     I    N

> A   L S  I G

> Y A   H R

> P     I





### Python solution

```python

class LeetcodeSolution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1 or numRows >= len(s): 
            return s
        row, direction, res = 0, -1, [""] * numRows
        for char in s:
            res[row] += char
            if row == 0 or row == numRows - 1: 
                direction *= -1 
            row += direction
        return "".join(res)

class MySolution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1 or numRows >= len(s):
            return s
        group_len = 2 * numRows - 2
        result = []
        index = 0
        for i in range(0, group_len // 2 + 1):
            index = i
            start_index = 0
            while index < len(s):
                if index % (group_len // 2) == 0:
                    result.append(s[index])
                else:
                    result.append(s[index])
                    if 2 * start_index - index + group_len < len(s):
                        result.append(s[2 * start_index - index + group_len])
                index += group_len
                start_index += group_len
        return "".join(result)

if __name__ == "__main__":
    print(LeetcodeSolution().convert("PAYPALISHIRING", 4))
    print(MySolution().convert("PAYPALISHIRING", 4))

```