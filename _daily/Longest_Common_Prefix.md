---
published: true
topic: Longest Common Prefix from LeetCode
subtitle: 
date: 2023-08-18
tags: Python LeetCode
---

# Longest Common Prefix from LeetCode

So, I'm a dumbass and just realised that coding could be an ok career path if I work my ass for it and
get good. Hence, it's time to being programming daily. Only problem is that:
1. I'm already gonna be pretty preoccupied with university, work, Chinese and Muay Thai pretty soon, so
I've gotta fit this in.
2. I suck and have a greater sense of how good I am at programming then I should

That being said, let's go!

### Horizontal Scanning Approach

The idea is to horizontally scan all the characters of the array of strings one by one, and find the
Longest Common Prefix among them.

#### Algoritmus
- Iterate through the strings one by one [0..N].
- For each iteration till ith index, LCP(S1, SI) can be obtained.
- If the LCP is an empty string, terminate the loop and return the empty string.
- Else, continue till end of list

### Vertical Scanning Approach
The idea is to scan and compare the characters from top to bottom of the ith index for each string.
If the LCP string is small, this is very efficient.

#### Algorithm
- Iterate through the string from S1 to SN,
- Start comparing ith indexes simultaneously for each string,
- If any of the ith indexes don't match, stop and return the current prefix
- Else, continue until end of list.

### Divide and Conquer Approach
The approach is to divide the given array of strings into various subproblems and merge them to get the LCP.

First, divide them into two parts. Then divide until the arrays become indivisible (i.e just two in each one).
Then, conquer, comparing common prefixes.

#### Algorithm
- Recursively divide the input array of strings into two parts,
- For each division, find the LCP obtained so far,
- Merge the obtained LCP from both the subarrays and return it.

### Binary Search Approach
We can use the concept of a binary search to attain the LCP.

#### Algorithm
- Consider the string with the smallest length, L,
- Consider the variables low=0 and high=L-1,
- Perform a [binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm):
  - Divide the string into two halves,
  - Compare the substring upto mid of this smallest string to every other character of the remaining strings
  at that index,
  - If the substring from 0 to mid-1 is common among all the substrings, update low with mid+1, otherwise
  update high with mid-1,
  - If low == high, terminate the algorithm and return the substring from 0 to mid.

And there we have it. Imma go implement one of these in leetcode now, just thought these were important
techniques I should keep in mind for future problems.
