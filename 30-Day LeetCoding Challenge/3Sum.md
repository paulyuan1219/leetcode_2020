# 3Sum
Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]

Sol1: brute force, time exceeded

```
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        L = len(nums)
        for i in range(L-2):
            for j in range(i+1, L-1):
                for k in range(j+1, L):
                    if nums[i] + nums[j] + nums[k] == 0:
                        tmp_tup = tuple(sorted([nums[i], nums[j], nums[k]]))
                        if tmp_tup not in res:
                            res.append(tmp_tup)

        return res
```

Sol2: Solve it using 2Sum

