+++
title = "LeetCode 1888. Minimum Number of Flips to Make the Binary String Alternating"
date = "2025-11-29"
author = "Max"
tags = ["leetcode", "sliding window", "medium"]
description = "Solve this medium-difficulty problem using the sliding window technique to find the minimum flips needed"
+++

## Problem Description

<a href="https://leetcode.com/problems/minimum-number-of-flips-to-make-the-binary-string-alternating/description/" target="_blank">📝 LeetCode Problem Link</a>

You are given a binary string s. You are allowed to perform two types of operations on the string in any sequence:

- Type-1: Remove the character at the start of the string s and append it to the end of the string. 
- Type-2: Pick any character in s and flip its value, i.e., if its value is '0' it becomes '1' and vice-versa.
Return the minimum number of `type-2 operations` you need to perform such that s becomes alternating.

The string is called alternating if no two adjacent characters are equal.
For example, the strings "010" and "1010" are alternating, while the string "0100" is not.

---
## Example 1:
```
Input: s = "111000"

Output: 2

Explanation: Use the first operation two times to make s = "100011".
Then, use the second operation on the third and sixth elements to make s = "101010".
```

---
## Problem understanding and initution you should have
1. the description says returning the minimum number of `type-2 operations`, which also means the type-1 operations are not important. Let's see what type-1 operation do (if we have s = "111000"): 
    ```
    - 111000 (0 time type-1 operation)
    - 110001 (1 time type-1 operation)
    - 100011 (2 times type-1 operation)
    - 000111 (3 times type-1 operation)
    - 001110 (4 times type-1 operation)
    - 011100 (5 times type-1 operation)
    - 111000 (6 times type-1 operation)
    ```

    You should be aware of the pattern of `circular array`! For circular array, we typically have two strategies: 1. use pointer to simulate (e.g. `s[i%n]`); 2. extend the original array (e.g. `s = s.extend(s)`).
2. if s = "111000", the result should be "010101" or "101010" (ground truth). What we can do? We can move the window (size of `n`) within the double sized `s`， and count how many flips we need to do. Can you imagine the sliding window trick now! When we move the window, we calculate the `right` pointer (if `s[right]` != it should be, flips += 1) and the `left` pointer (if `s[left]` != it should be, flips -= 1)

---
## How it works?

```
s = "111000"
s+s = "111000111000"

Window:        [111000]111000
Ground truth1: [010101]010101 (4 flips, at index 0, 2, 3, 5)
Ground truth2: [101010]101010 (2 flips, at index 1, 4)

Window:         1[110001]11000
Ground truth1:  0[101010]10101 (4 flips, at index 1, 2, 4, 5)
Ground truth2:  1[010101]01010 (2 flips, at index 0, 3)
```

[`1`1100`0`]  
&nbsp;`l`&nbsp;&nbsp;&nbsp;&nbsp;`r`

Entering window: when we move right pointer, check the current right pointer equals to the ground truth or not, and do something; Leaving window: when we move left pointer, check the current left pointer equals to ground truth or not, and do something

In fact, we only need one variable to keep track of the flips in the sliding window! Once you transform the question, the implementation should be quiet easy.

--- 
## My solution
```python
class Solution:
    def minFlips(self, s: str) -> int:
        ans = float('inf')
        cnt = 0 
        n = len(s)
        for i in range(2 * n):
            if int(s[i%n]) % 2 != i % 2: # entering window
                cnt += 1

            left = i - n + 1
            if left < 0:
                continue
            ans = min(ans, cnt, n-cnt)
            if int(s[left%n]) % 2 != left % 2: # levaing window
                cnt -= 1
        
        return ans
```

--- 
## Summary and thoughts
1. find initution (need time to sink in, as long as you did enough leetcode questions, you know what kind of pattern it is and what kind of tricks you need to perform on this question): for this question, it will be circular array.
2. notice the hint: why only type-2 operations matter? Even if you know the trick (circular array), you need to find a way to use it. This question basically says, using the circular array!
3. It is a hard-medium I think, pretty tricky. <a href="https://leetcode.cn/discuss/post/3578981/ti-dan-hua-dong-chuang-kou-ding-chang-bu-rzz7/" target="_blank">Difficulty Score: 2006</a>. Here I suggest this blogger <a href="https://leetcode.cn/u/endlesscheng/" target="_blank">灵山爱茶府</a>, he rated lots of questions, you could refer to it. `A good point: never choose hard questions to beat your initiative and never choose easy questions to let your brain being lazy.` I think once you follow his lists, you will need what these scores mean to you. As a reference, I will tell you I did 400 questions on LeetCode and I think my level is around 1800 scores (I mean not hard and not easy), for beginner you should focus on <1600 scores.