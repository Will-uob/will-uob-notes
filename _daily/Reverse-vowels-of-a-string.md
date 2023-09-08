---
title: Reverse vowels of a string
published: true
date: 2023-09-08
tags: Leetcode Programming
---

## Problem description
Given a string ```s```, reverse only all the vowels in the string and return it.

The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both lower and upper cases, more than once.

#### Example 1:
```
Input: s = "hello"
Output: "holle"
```
#### Example 2:
```
Input: s = "leetcode"
Output: "leotcede"
```

Constraints:
- ```1 <= s.length <= 3 * 105```
- ```s``` consist of printable ASCII characters.

## My solution
Is pretty bad to be honest. It's simple, but not very fast or memory efficient.

```
class Solution:
    def reverseVowels(self, s: str) -> str:
        getVowels = [x for x in s if self.isVowel(x)]
        newS = list(s)
        count = 1
        for i in range(0, len(s)):
            if self.isVowel(s[i]):
                newS[i] = getVowels[-count]
                count += 1
        return ''.join(newS)

    def isVowel(self, letter: str) -> bool:
        if letter.lower() in ['a', 'e', 'i', 'o', 'u']:
            return True
        else:
            return False
```

I believe this is $O(n)$ time complexity, though I could definitely be wrong about that.

## Their solution
Is very nice and elegant. They use the two pointers technique: one pointer starting from the beginning of the string and another starting from the end. They move these pointers towards each other,
swapping the vowels they point to until they meet in the middle of the string[^1].

```
class Solution(object):
    def reverseVowels(self, s):
        # Convert the input string to a character array.
        word = list(s)
        start = 0
        end = len(s) - 1
        vowels = "aeiouAEIOU"

        # Loop until the start pointer is no longer less than the end pointer.
        while start < end:
            # Move the start pointer towards the end until it points to a vowel.
            while start < end and vowels.find(word[start]) == -1:
                start += 1

            # Move the end pointer towards the start until it points to a vowel.
            while start < end and vowels.find(word[end]) == -1:
                end -= 1

            # Swap the vowels found at the start and end positions.
            word[start], word[end] = word[end], word[start]

            # Move the pointers towards each other for the next iteration.
            start += 1
            end -= 1

        # Convert the character array back to a string and return the result.
        return "".join(word)
```

### Time and Space Complexity of their solution
The time complexity of their solution is $O(n)$, where $n$ is the length of the input string $s$. The space complexity is $O(n)$.

[^1]: See sorting and searching algorithms, as this reminds of them, especially insertion sort. Christ, there is so much I've forgotten over the last few years! This shit is cool!

