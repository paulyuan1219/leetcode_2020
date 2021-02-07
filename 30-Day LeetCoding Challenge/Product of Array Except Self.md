Product of Array Except Self

Given an array nums of n integers where n > 1,  return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Example:

Input:  [1,2,3,4]
Output: [24,12,8,6]
Constraint: It's guaranteed that the product of the elements of any prefix or suffix of the array (including the whole array) fits in a 32 bit integer.

Note: Please solve it without division and in O(n).

Follow up:
Could you solve it with constant space complexity? (The output array does not count as extra space for the purpose of space complexity analysis.)

Solution 1: ~90

最直接的做法。如果nums中的零的个数超过两个，那么返回零向量。如果完全没有零，就可以用除法来做。如果只有一个零，那么只需要处理这个元素即可。这个方法是最快的，但是不符合题目的限定。因为使用了除法。

```
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = 1
        zero_count = 0
        for num in nums:
            if num == 0:
                zero_count += 1
            else:
                res *= num
        
        if zero_count >= 2:
            return [0] * len(nums)
        elif zero_count == 0:
            return [res/num for num in nums]
        else:
            nums1 = []
            for num in nums:
                if num != 0:
                    nums1.append(0)
                else:
                    nums1.append(res)
            return nums1
```

Solution 2:  超时了

不使用除法，那么就只能使用乘法了。尝试只用乘法，但是n^2的方法，超时了

```
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        res = [1] * len(nums)
        
        for i, num in enumerate(nums):
            for j,r in enumerate(res):
                if j != i:
                    res[j] = r*num
        return res
```
如果只是直接用乘法，那么肯定有问题，因为最终，每个元素的得到都需要n个乘法，所以最终的复杂度一定是n^2

现在的突破口只能是重复项，因为不同的乘法中有大量的重复操作，我们应该想法把现有的想法利用出来。

Solution 3: ~19

进一步想想，每个位置的最终结果，其实可以分成左右两部分。所以我们只需要从左往右遍历一次，拿到每一个位置左侧的乘积。再从右往左遍历一次，拿到每一个位置右侧的乘积。最终把这两个list配对相乘就可以了。

```
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        
        arr_left = [1] * len(nums)
        left_cum = 1
        for i in range(1, len(nums)):
            left_cum *= nums[i-1]
            arr_left[i] = left_cum
        arr_right = [1] * len(nums)
        right_cum = 1
        for i in range(len(nums)-2, -1, -1):
            right_cum *= nums[i+1]
            arr_right[i] = right_cum
        
        return [x*y for x,y in zip(arr_left, arr_right)]
```

Solution 4: ~77

进一步思考follow up。我们发现，Solution 3中其实没必要使用两个list。我们完全只使用一个list。首先从左向右更新每个元素，然后再葱油往左更新每个元素即可。

```
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        
        arr_left = [1] * len(nums)
        left_cum = 1
        for i in range(1, len(nums)):
            left_cum *= nums[i-1]
            arr_left[i] = left_cum
            
        right_cum = 1
        for i in range(len(nums)-2, -1, -1):
            right_cum *= nums[i+1]
            arr_left[i] *= right_cum
        return arr_left
```


