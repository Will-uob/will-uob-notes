---
title: Leetcode: Merge Strings Alternately
date: 06-09-2023
published: true
tags: Leetcode Programming Python C++
---

## Problem description
You are given two strings word1 and word2. Merge the strings by adding letters in alternating order,
starting with word1. If a string is longer than the other, append the additional letters onto the end
of the merged string.

Return the merged string.

#### Example 1:
```
Input: word1 = "abc", word2 = "pqr"
Output: "apbqcr"
Explanation: The merged string will be merged as so:
word1:  a   b   c
word2:    p   q   r
merged: a p b q c r
```

#### Example 2:
```
Input: word1 = "ab", word2 = "pqrs"
Output: "apbqrs"
Explanation: Notice that as word2 is longer, "rs" is appended to the end.
word1:  a   b
word2:    p   q   r   s
merged: a p b q   r   s
```

#### Example 3:
```
Input: word1 = "abcd", word2 = "pq"
Output: "apbqcd"
Explanation: Notice that as word1 is longer, "cd" is appended to the end.
word1:  a   b   c   d
word2:    p   q
merged: a p b q c   d
```

#### Constraints:
- ```1 <= word1.length, word2.length <= 100```
- ```word1``` and ```word2``` consist of lowercase English letters.

## My solution
Works. I think it's quite a verbose solution, and uses a little too much memory for my liking, but
it's actually quite nice. Plus, I believe this is working in $O(n)$ time, which is great!

```
class Solution:
    def mergeAlternately(self, word1: str, word2: str) -> str:
        newstr = ""
        if len(word1) <= len(word2):
            count = 0
            for i in range(0, len(word1)):
                newstr += word1[i]
                newstr += word2[i]
                count += 1
            newstr += word2[i+1:]
        else:
            count = 0
            for i in range(0, len(word2)):
                newstr += word1[i]
                newstr += word2[i]
                count += 1
            newstr += word1[i+1:]
        return newstr
```

### Solutions of others in Python
The solution I found which was the nicest was the following:
```
class Solution(object):
    def mergeAlternately(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: str
        """
        result = []
        i = 0
        while i < len(word1) or i < len(word2):
            if i < len(word1):
                result.append(word1[i])
            if i < len(word2):
                result.append(word2[i])
            i += 1
        return ''.join(result) # What does this do?
```

It's a very similar idea to mine, just implemented differently.

### Solutions of others in C++
Since the language I want strongest to be after Python is C++, indeed I probably need a good
understanding of:
- Python
- C/C++
- SQL
- Typescript?
in order to become a more well-rounded programmer. However, at the moment the focus is of course
Python.

```
class Solution {
public:
    string mergeAlternately(string word1, string word2) {
        string result = "";
        int i = 0;
        while (i < word1.length() || i < word2.length()) {
            if (i < word1.length()) {
                result += word1[i];
            }
            if (i < word2.length()) {
                result += word2[i];
            }
            i++;
        }
        return result;
    }
};
```
This solution is once again very similar to above.

### What is Python's .join() method?
Joins elements from the iterable separated by a string operator.

#### Examples:
```
numlist = [1, 3, 5, 7, 9]
separator = ', '
print(separator.join(numlist))

words = ['Hello','can','we', 'play', 'today', '!']
sentence = ' '.join(words)
print(sentence)
```

### Using a join method with Python Sets.
A set in Python is defined by the following features:
- Sets are unordered,
- Set elements are unique, duplicate elements are not allowed,
- A set itself might be modified, but the elements within the set must be
  immutable (unchanging).

#### Example usage
```
set1 = {'Mumbai', 'Delhi', 'New York'}
a = ' -> '
print('Flight Route:', a.join(set1))

set2 = {'a', 'e', 'i', 'o', 'u'}
b = ''
print('Vowel characters are:', b.join(set2))
```
