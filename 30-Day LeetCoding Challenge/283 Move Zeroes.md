Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]

Note:

+ You must do this in-place without making a copy of the array.
+ Minimize the total number of operations.

Solution on April 4th, 2020

I use a 2 pointer method to solve the problem.

First, let p1 point to the first zero position. This is the slot position where a future non-zero number can fit in.
Second, let p2 point to the first non-zero position after p1. This is the slot position where nums[p2] should be moved to position p1.
After that, nums[p2] should be set to 0. Therefore, next time when we keep moving p1 and when p1 meets this position, it's already 0 such that 
p1 will just keep moving.

It's straightforward to move p1 from left to right. But be careful for p2. Since p2 is also moving to right, and sometimes p1 might just keep moving and pass the original value of p2.
So we must set p2 = max(p1+1, p2+1).

    class Solution(object):
        def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        if len(nums) == 0:
            return
        
        p1 = 0
        p2 = 0

        while True:
            while p1 < len(nums) and nums[p1] != 0:
                p1 += 1
            if p1 == len(nums):
                return
            
            p2 = max(p1+1, p2+1)
            while p2 < len(nums) and nums[p2] == 0:
                p2 += 1
            if p2 == len(nums):
                return

            nums[p1] = nums[p2]
            nums[p2] = 0
            
            p1+=1
            
