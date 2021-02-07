# Single Element in a Sorted Array


You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once. Find this single element that appears only once.

 

Example 1:

```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

Example 2:

```
Input: [3,3,7,7,10,11,11]
Output: 10
``` 

Note: Your solution should run in O(log n) time and O(1) space.

Solution:

根据提示，用二分法来做就可以。只是中间的边界判断要当心，我一开始错了好几次，后来仔细想才想明白，得到下面的结果

```
class Solution(object):
    def singleNonDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        """
        if len(nums) == 1:
            return nums[0]
        
        if len(nums) == 3:
            if nums[0] == nums[1]:
                return nums[2]
            else:
                return nums[0]
        """
        
        l = 0
        r = len(nums)-1
        
        while l < r: # boil down to 3 elements
            mid = int((l+r)/2)
            
            if nums[mid] != nums[mid-1] and nums[mid] != nums[mid+1]:
                return nums[mid]
            else:
                if nums[mid] == nums[mid-1]:
                    if (mid-l)%2 == 0: # odd elems from l to mid
                        r = mid - 2
                    else:
                        l = mid + 1
                elif nums[mid] == nums[mid+1]:
                    if (r-mid)%2 == 0: # odd elems from mid to r
                        l = mid + 2
                    else:
                        r = mid - 1
        return nums[l]
```

