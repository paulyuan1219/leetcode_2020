Contiguous Array
Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
Example 2:
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
Note: The length of the given binary array will not exceed 50,000.

Solution 1: Time limit exceed

Most straightforward way

```
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) < 2:
            return 0
        
        res = 0
        for i in range(len(nums)-1):
            for j in range(i+1, len(nums)):
                curr_len = j-i+1
                
                if curr_len %2 == 1:
                    continue
                
                curr_sum = sum(nums[i:j+1])
                if curr_sum == curr_len / 2:
                    if res < curr_len:
                        res = curr_len
        return res

```
Solution 2: Time exceeds

下面，我想用递归的方法写，

```
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        def help(arr, i, j):
            N = j - i
            
            if N < 2:
                return 0

            curr_sum = sum(arr[i:j])
            
            if N%2 == 0 and curr_sum == N/2:
                # this means N is even and half of the array is 0
                return N
            
            if float(curr_sum) < float(N)/2:
                criteria = 0
            else:
                criteria = 1
            
            # more 0 than 1
            k1 = i
            while k1 < j and arr[k1] != criteria:
                k1 += 1
            # now, k1 points to the leftest criteria
            k2 = j -1 
            while k2 >= i and arr[k2] != criteria:
                k2 -= 1
            # now, k2 points to the rightest criteria
            return max(help(arr, k1+1, j), help(arr, i, k2))
        
        return help(nums, 0, len(nums))
```

Solution 3:

参考了官方的解法2 居然还是不行？

```
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        N = len(nums)
        arr = [None] * (2*N+1)
        res = 0
        
        curr_status = 0
        
        for i in range(len(nums)):
            if nums[i] == 0:
                curr_status -= 1
            else:
                curr_status += 1
            
            if arr[curr_status] is None:
                arr[curr_status] = i
                continue
            else:
                curr_len = i - arr[curr_status]
                if res < curr_len:
                    res = curr_len

        return res

```

Solution 4: 

This is the most popular python solution in discussion

```
class Solution(object):
    def findMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        count = 0
        max_length=0
        table = {0: 0}
        for index, num in enumerate(nums, 1):
            if num == 0:
                count -= 1
            else:
                count += 1
            
            if count in table:
                max_length = max(max_length, index - table[count])
            else:
                table[count] = index
        
        return max_length
```






下面这个想法只能说是借鉴 但是实际上想不出该怎么用 呵呵。

This is must like the max sum subarray problem. I think I can use a 2 pointer way to do that.

基本的想法好像还是维护两个指针，先固定左侧的i，向右寻找最大可能，然后固定右侧的j。然后再陆续把左侧的i依次向右推动，不断寻找最大子串即可。

