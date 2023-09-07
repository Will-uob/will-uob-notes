---
published: true
title: How do you calculate the greatest common divisor of strings?
date: 2023-09-07
tags: Leetcode Programming
---

## Problem description
For two strings s and t, we say "t divides s" if and only if s = t + ... + t (i.e., t is concatenated with itself one or more times).

Given two strings str1 and str2, return the largest string x such that x divides both str1 and str2.

#### Example 1:

Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"

#### Example 2:

Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"

#### Example 3:

Input: str1 = "LEET", str2 = "CODE"
Output: ""

#### Constraints:
- 1 <= str1.length, str2.length <= 1000
- str1 and str2 consist of English uppercase

### My attempted solution
Was terrible. The idea was to take all substrings of the shorter string, that were at most half the size of the shorter string. Then, we manually check each one to see
if a multiple of the string is indeed a match to our original strings, ```str1``` and ```str2```. This is, of course, a lot of badness, and took far too much time to process.

### Their solution
Was very elegant. Indeed, it's only six lines:
```
import math
class Solution:
    def gcdOfStrings(self, str1: str, str2: str) -> str:
        if (str1 + str2) == (str2 + str1): # This ensures that each string is comprised of a mutual substring,
        # otherwise, concatenation of these substrings would be impossible.
            return str1[:gcd(len(str1), len(str2))] # Gets the substring of length which is the greatest common divisor between
            # str1 and str2
        else:
            return ""
```

### List comprehensions in Python
List comprehensions offer an alternative way of constructing lists based on conditions.

#### Syntax
The syntax is as follows:
``` newlist = [expression for item in iterable if condition == True] ```

Note that there are some key points to be made here:
- the condition can be left blank,
- the iterable is... well anything iterable!!
- the expression is the current item in the iteration, but also
  the outcome, meaning we can manipulate it before it ends up like
  a list item in the new list.

Come to think of it, these are all very similar to Haskell...

#### Example
```
fruits = ["apple", "banana", "cherry", "kiwi", "mango"]
newlist = [x for x in fruits if "a" in x]
print(newlist)
```

### What about nested list comprehensions in Python?
Nested List Comprehensions are just list comprehensions within list comprehensions. For example,
suppose we want to generate a matrix. We could use for loops, but these are untidy and long-winded.
Instead, we can use a nested list comprehensions, like so:
```
matrix = [[j for j in range(5)] for i in range(5)]
print(matrix)
```

### Another example: Flattening a matrix
We could flatten a matrix with two for loops, but there is a nicer way, using list comprehensions:
```
matrix = [[1,2,3], [4,5], [6,7,8,9]]
flatten_matrix = [val for sublist in matrix for val in sublist]
print(flatten_matrix)
```

which is easier to read if we break it up into the following format:
```
flatten_matrix = [val # The value we want to append to the list
                   for sublist in matrix # The outer loop
                   for val in sublist] # The inner loop
```
