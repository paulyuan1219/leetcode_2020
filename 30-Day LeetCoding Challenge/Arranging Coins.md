# Arranging Coins
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:

n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
Example 2:

n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.


## sol1. Error

```
class Solution(object):
    def arrangeCoins(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0:
            return 0
        elif n == 1:
            return 1
        
        num_rows = 0
        num_elem = 0
        for i in range(1, n+1):
            
            if num_elem + i > n:
                return num_rows

            num_rows += 1
            num_elem += i
        
        return num_rows
```

Submission Result: Runtime Error 

```
Runtime Error Message:
MemoryError
    for i in range(1, n+1):
Line 14 in arrangeCoins (Solution.py)
    ret = Solution().arrangeCoins(param_1)
Line 49 in _driver (Solution.py)
    _driver()
Line 59 in <module> (Solution.py)
Last executed input:
1804289383            
```

            
            
        
        
        
        
        