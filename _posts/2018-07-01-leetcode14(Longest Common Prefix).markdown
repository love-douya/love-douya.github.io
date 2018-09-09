---
layout: post
title:  "Longest Common Prefix(Leetcode14)"
date:   2018-07-01 19:06:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

### Example 1

>* Input: ["flower","flow","flight"]
>* Output: "fl"

### Example 2

>* Input: ["dog","racecar","car"]
>* Output: ""
>* Explanation: There is no common prefix among the input strings.





### Python solution

```python

class Solution:
    def pop_char(self, Common_Prefix, pop_number):
        Number = 0
        while Number != pop_number:
            Common_Prefix.pop()
            Number += 1
        #return Common_Prefix

    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        Common_Prefix = []
        #length_of_Set = 0
        String_Num = len(strs)
        try:
            String_Len = min([len(strs[i]) for i in range(String_Num)])
        except Exception:
            return ""
        else:
            for i in range(0, String_Len):
                for j in range(0, String_Num):
                    Common_Prefix.append(strs[j][i])
                #Common_Prefix_temp = copy.deepcopy(Common_Prefix)
                if len(set(Common_Prefix[-(String_Num):])) == 1:
                    print(Common_Prefix[-(String_Num):])
                    #length_of_Set = len(set(Common_Prefix))
                    self.pop_char(Common_Prefix, String_Num - 1)
                    print(Common_Prefix)
                else:
                    self.pop_char(Common_Prefix, String_Num)
                    print(Common_Prefix)
                    break
            #return "".join(list(OrderedDict.fromkeys(Common_Prefix)))
            return "".join(Common_Prefix)

```