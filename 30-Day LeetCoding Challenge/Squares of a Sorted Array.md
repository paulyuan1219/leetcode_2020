# Squares of a Sorted Array

Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

 

Example 1:

```
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```

Example 2:

```
Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
``` 

Note:

+ 1 <= A.length <= 10000
+ -10000 <= A[i] <= 10000
+ A is sorted in non-decreasing order.


Solution 1:

```
class Solution(object):
    def sortedSquares(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        B = [x**2 for x in A]
        return sorted(B)
```

Solution 2:

开始审题的时候，没注意A是排好序的。所以大致看了答案之后，用一个双指针明显更加快。

```
class Solution(object):
    def sortedSquares(self, A):
        """
        :type A: List[int]
        :rtype: List[int]
        """
        i = 0
        while i < len(A) and A[i] < 0:
            i += 1
            
        if i == len(A):
            # this means the whole A is less than 0
            return [x**2 for x in A][::-1]
        
        
        if i == 0:
            # this means the whole A is larger than 0
            return [x**2 for x in A]
        
        # here, we know that A[i] is the first positive, A[i-1] is the previous negative
        
        res = []
        j = i
        i = i-1
        while i >=0 and j < len(A):
            i2 = A[i]**2
            j2 = A[j]**2
            if i2 <= j2:
                res.append(i2)
                i -= 1
            else:
                res.append(j2)
                j += 1
        while i >= 0:
            res.append(A[i]**2)
            i -= 1
        
        while j < len(A):
            res.append(A[j]**2)
            j += 1
        return res
```