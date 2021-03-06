# Search Insert Position

Solution
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Example 1:

Input: [1,3,5,6], 5
Output: 2
Example 2:

Input: [1,3,5,6], 2
Output: 1
Example 3:

Input: [1,3,5,6], 7
Output: 4
Example 4:

Input: [1,3,5,6], 0
Output: 0


Solution: Trival

```
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        
        if len(nums) == 0:
            return 0
        
        if target < nums[0]:
            return 0
        
        if target > nums[-1]:
            return len(nums)
        
        # now we know nums[0] <= target <= nums[-1]
        p = 0
        while p < len(nums) and nums[p] <= target:
            p += 1
        
        # if here, we know nums[p] > target
        # then, nums[p-1] <= target
        if nums[p-1] == target:
            return p-1
        else:
            return p
        
        
```