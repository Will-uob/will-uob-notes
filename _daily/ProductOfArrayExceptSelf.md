---
published: true
date: 2023-09-09
title: Product of array except self
tags: Leetcode Programming
---

I've completed two problems today so far, but the first one took a while cause I was being stupid. I did manage to get a one line, pythonic solution, however, so that was nice!

## Problem description
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in $O(n)$ time and without using the division operation.
```
Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]

Example 2:

Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

Constraints:

- ```2 <= nums.length <= 105```
- ```-30 <= nums[i] <= 30```
- The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

## Answers
The following contains both my answer, which was too slow, though it did complete the task using brute force, and the solution provided by [Algo Engine](https://www.youtube.com/watch?time_continue=406&v=5bS636lE_R0&embeds_referring_euri=https%3A%2F%2Fleetcode.com%2F&source_ve_path=MjM4NTE&feature=emb_title).

```
import math
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        """
        answer = []
        for i in range(0, len(nums)-1):
            answer.append(math.prod(nums[0:i] + nums[i+1:]))
        answer.append(math.prod(nums[:-1]))
        return answer
        """

        length = len(nums)
        products = [1] * length
        for i in range(1, length):
            products[i] = products[i-1] * nums[i-1]

        right = nums[-1]
        for i in range(length-2, -1, -1):
            products[i] *= right
            right *= nums[i]

        return products
```

### Explanation of AlgoEngine's code

![This is a diagram of the idea](/images/AlgoEngine1.png)

The basic idea is that each yellow sum is the product of a left and right array. Noticing this, we can save a lot of time and effort by using product we've already calculated, first on the left-hand side and
then on the right hand side, by reusing that we've calculated before.
