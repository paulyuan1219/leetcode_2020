# Maximum Sum Circular Subarray

Given a circular array C of integers represented by A, find the maximum possible sum of a non-empty subarray of C.

Here, a circular array means the end of the array connects to the beginning of the array.  (Formally, C[i] = A[i] when 0 <= i < A.length, and C[i+A.length] = C[i] when i >= 0.)

Also, a subarray may only include each element of the fixed buffer A at most once.  (Formally, for a subarray C[i], C[i+1], ..., C[j], there does not exist i <= k1, k2 <= j with k1 % A.length = k2 % A.length.)

 

Example 1:

```
Input: [1,-2,3,-2]
Output: 3
Explanation: Subarray [3] has maximum sum 3
```

Example 2:

```
Input: [5,-3,5]
Output: 10
Explanation: Subarray [5,5] has maximum sum 5 + 5 = 10
```

Example 3:

```
Input: [3,-1,2,-1]
Output: 4
Explanation: Subarray [2,-1,3] has maximum sum 2 + (-1) + 3 = 4
```

Example 4:

```
Input: [3,-2,2,-3]
Output: 3
Explanation: Subarray [3] and [3,-2,2] both have maximum sum 3
```

Example 5:

```
Input: [-2,-3,-1]
Output: -1
Explanation: Subarray [-1] has maximum sum -1
``` 

Note:

+ -30000 <= A[i] <= 30000
+ 1 <= A.length <= 30000


Solution 1: Bruteforce, Time limit exceeded.

```
class Solution(object):
    def maxSubarraySumCircular(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        N = len(A)
        
        res = -100000000
        for i in range(N):
            # set i as the starting index
            tmp_sum = 0
            for j in range(N):
                index = (i+j) % N
                tmp_sum += A[index]
                if res < tmp_sum:
                    res = tmp_sum
        
        return res
```

下面这个方法稍微改进了一下，但是还是不够

```
class Solution(object):
    def maxSubarraySumCircular(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        N = len(A)
        
        res = -100000000
        for i in range(N):
            # set i as the starting index
            tmp_sum = 0
            for j in range(i, N):
                tmp_sum += A[j]
                if res < tmp_sum:
                    res = tmp_sum
            
            for j in range(i):
                tmp_sum += A[j]
                if res < tmp_sum:
                    res = tmp_sum
        return res
```

暂时先放一放吧 感觉上，应该使用dp或者贪心的思路来做。好像就是这样。之前应该做过不带循环的版本。也就是说，当考虑i的时候，只要考虑i本身以及i-1之前的是否最大化 呵呵。不难

然后照抄了一个别人的答案，先这样吧 

```
class Solution(object):
    def maxSubarraySumCircular(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        if max(A) <= 0: return max(A)
        endmax = [i for i in A]
        endmin = [i for i in A]
        for i in xrange(1,len(A)):
            if endmax[i-1] > 0: endmax[i] += endmax[i-1]
            if endmin[i-1] < 0: endmin[i] += endmin[i-1]

        return max(max(endmax),sum(A) - min(endmin))
```
