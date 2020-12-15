# Pow(x, n)

Implement pow(x, n), which calculates x raised to the power n (xn).

Example 1:

Input: 2.00000, 10
Output: 1024.00000
Example 2:

Input: 2.10000, 3
Output: 9.26100
Example 3:

Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
Note:

-100.0 < x < 100.0
n is a 32-bit signed integer, within the range [−231, 231 − 1]


Sol1: overflow problem

```
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        
        bPositive = True
        if n < 0:
            bPositive = False
            n = -n
        
        res = 1
        for i in range(n):
            res = res * x
        
        if bPositive:
            return res
        else:
            return 1 / res
```

```
Runtime Error Message:
MemoryError
    for i in range(n):
Line 15 in myPow (Solution.py)
    ret = Solution().myPow(param_1, param_2)
Line 46 in _driver (Solution.py)
    _driver()
Line 56 in <module> (Solution.py)
Last executed input:
0.00001
2147483647        
```

