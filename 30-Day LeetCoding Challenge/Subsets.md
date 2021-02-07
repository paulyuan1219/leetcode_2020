# Subsets

Solution
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

Sol1:

最简单的方法，假设数组长度为N，那么一共的可能性 2^N, which can be represented using a binary string

```
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        N = len(nums)
        
        for i in range(2**N):
            i_binary = "{0:b}".format(i)
            if len(i_binary) < N:
                i_binary = '0'*(N-len(i_binary)) + i_binary
            
            tmp_res = [nums[j] for j in range(N) if i_binary[j] == "1"]
            res.append(tmp_res)
        return res
```