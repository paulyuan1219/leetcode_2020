Given a binary array, find the maximum number of consecutive 1s in this array.

Example 1:
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
Note:

The input array will only contain 0 and 1.
The length of input array is a positive integer and will not exceed 10,000

Solution:

Just use 2 pointer in each stage. This is fast enough

```
class Solution(object):
    def findMaxConsecutiveOnes(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i = 0
        res = 0
        while True:
            while i < len(nums) and nums[i] == 0:
                i += 1
            
            if i == len(nums):
                return res
            
            # now nums[i] is the first one we see in this stage
            j = i + 1
            while j < len(nums) and nums[j] == 1:
                j += 1
            
            # now j is out of index, or point to the first seen zero
            curr_len = j-i
            if res < curr_len:
                res = curr_len
            
            if j >= len(nums):
                return res
            else:
                i = j + 1
```
