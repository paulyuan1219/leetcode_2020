# Find the Duplicate Number
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Example 1:

Input: [1,3,4,2,2]
Output: 2
Example 2:

Input: [3,1,3,4,2]
Output: 3
Note:

You must not modify the array (assume the array is read only).
You must use only constant, O(1) extra space.
Your runtime complexity should be less than O(n2).
There is only one duplicate number in the array, but it could be repeated more than once.

Sol1: Error

```
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res = 0
        
        for num in nums:
            if res == 0:
                res = num
            elif res == num:
                return res
            else:
                res = 0
        return res
```

Submission Result: Wrong Answer 
Input:
[3,1,3,4,2]
Output:
2
Expected:
3

好吧 大意了

Sol2: sort first

```
class Solution(object):
    def findDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        if len(nums) <=2:
            return nums[0]
        
        nums1 = sorted(nums)
        for i in range(1, len(nums1)):
            if nums1[i-1] == nums1[i]:
                return nums1[i]
        return
```