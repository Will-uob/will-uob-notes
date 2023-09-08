---
published: true
title: Can place flowers
date: 2023-09-08
tags: Leetcode Programming
---

## Problem description
You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.

Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the flowerbed without violating the
no-adjacent-flowers rule and false otherwise.
```
Example 1:

Input: flowerbed = [1,0,0,0,1], n = 1
Output: true

Example 2:

Input: flowerbed = [1,0,0,0,1], n = 2
Output: false
```

Constraints:

- ```1 <= flowerbed.length <= 2 * 104```
- flowerbed[i] is 0 or 1.
- There are no two adjacent flowers in flowerbed.
- ```0 <= n <= flowerbed.length```

### My 1st attempt at a solution
My first solution was pretty clumsy, but works!

```
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        # badPatterns = [[1,0,1], [1,0,1]]
        validPlots = 0
        i = 0
        # Could another approach be to check from the sides and go inwards?
        if (len(flowerbed) == 1):
            if flowerbed[i] == 0:
                validPlots += 1
        else:
            if (flowerbed[i] == 0 and flowerbed[i+1] == 0):
                validPlots += 1
                flowerbed[i] = 1
                i += 2
            while (i <= len(flowerbed)-2):
                if flowerbed[i] == 1:
                    i += 1
                else:
                    if flowerbed[i-1] == 0 and flowerbed[i+1] == 0:
                        validPlots += 1
                        flowerbed[i] = 1
                        i += 2
                    else:
                        i += 1
            if (flowerbed[-1] == 0 and flowerbed[-2] == 0):
                validPlots += 1
                flowerbed[-1] = 1
        return (validPlots >= n)
```

I think the time complexity is $O(n)$, with the space complexity a constant, $O(1)$.

### My second attempt at a solution
Was supposed to be less clumsy, and focused on the idea of breaking down the list from both sides. It is not yet finished, so I'm only putting
it here so I can remember to do it later.

```
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        # badPatterns = [[1,0,1], [1,0,1]]
        validPlots = 0
        Left = 0
        Right = 0
        # Eat the matrix, checking the sides along the way to see if we have a possible plot
        while (len(flowerbed) > 3):
            if self.isValidCorner(flowerbed[:2]) == 0:
                Left = 0
                validPlots += 1
            else:
                Left = self.isValidCorner(flowerbed[:2])
            if self.isValidCorner(flowerbed[-2:]) == 0:
                Right = 0
                validPlots += 1
            else:
                Right = self.isValidCorner(flowerbed[-2:])
            flowerbed = flowerbed[2:-2]

        # We are now left with four cases, a list of size 0,1,2 or 3. We only consider 1,2 and 3
        if (len(flowerbed) == 1):
            if flowerbed[0] == 0:
                validPlots += 1
        elif (len(flowerbed) == 2):
            if flowerbed == [0,0]:
                validPlots += 1
        else: 
            if flowerbed == [0,0,0]:
                validPlots += 1
            else:
                if flowerbed == [1,0,0] and (Right == 2 or Right == 0):
                    validPlots += 1
                elif flowerber == [0,0,1] and (Left == 1 or Left == 0):
                    validPlots += 1

        
        return (validPlots >= n)

    def isValidCorner(self, corner: List[int]) -> int:
        match corner:
            case [0,0]:
                return 0
            case [1,0]:
                return 1
            case [0,1]:
                return 2
            case [1,1]:
                return 3
```

### A better solution
This is so elegant it's not even funny. Like, wow! Time complexity appears to be $O(n)$, while the space complexity seems to be $O(1)$.
```
class Solution:
    def canPlaceFlowers(self, flowerbed: List[int], n: int) -> bool:
        if n == 0:
            return True
        for i in range(len(flowerbed)):
            if flowerbed[i] == 0 and (i == 0 or flowerbed[i-1] == 0) and (i == len(flowerbed)-1 or flowerbed[i+1] == 0):
                flowerbed[i] = 1
                n -= 1
                if n == 0:
                    return True
        return False
```
