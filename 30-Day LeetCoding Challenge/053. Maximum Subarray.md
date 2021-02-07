Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

Solution:

I didn't solve the problem on my own. Instead, I refer to a great video at <https://www.youtube.com/watch?v=86CQq3pKSUw>

For a bruteforce approach, given a list of n elements, there are O(n^2) different subarrays. For example, starting from position-0, we have n subarrays like [0,0],[0,1],[0,2]...[0,n-1]. Staring fro position-1, we have n-1 subarrays lik [1,1], [1,2], ..., [1, n-1]. You get the idea. <br>

Overall, there are O(n^2) subarrays, and we have to get the sum of everyone, then we can know the largest one.

The Kadane's algorithm works in a reverse manner. The basic idea is as follows. 
+ With ending-position-0, we have 1 subarray like [0,0]. 
+ With ending-position-1, we have 2 subarray [0,1],[1,1]. 
+ With ending-position-2, we have 3 subarray [0,2] [1,2] [2,2]
+ ...
+ With ending-position-(n-1), we have n subarray [0,n-1] [1,n-1] [2,n-1] ...  [n-1,n-1]
Again, we need to compute the sum of each subarray to get the largest sum.

However, Kadane proved the following stuff:
+ With ending-position-k, we have k+1 subarray [0,...,k-1,k] [1,...,k-1,k] [2,...,k-1,k] ... [k-1,k] [k]
+ Suppose we already know that for ending-position-(k-1), the largest sum subarray is T, i.e. something like [i,...,k-1]
+ Then for ending-position-k, the lagest sum subarray can only be T+k ([i, ..., k-1, k]) or k ([k]). There's no other possibility.
+ The proof is simple. Suppose there's a conflict. There's a subarray T'=[j,...,k-1] and j<>i and sum(T') > sum(T), then T is no longer the largest sum subarray of T. Conflict found. Proved.
+ Therefore, at each ending-position, we only need t compute and compare 2 values. The total algorithm runs in linea.

```
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        
        res_max = nums[0]
        curr_max = nums[0]
        
        for i in range(1, len(nums)):
            curr_max = max(nums[i], curr_max+nums[i])
            if res_max < curr_max:
                res_max = curr_max
        return res_max
```





