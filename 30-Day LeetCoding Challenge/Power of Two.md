# Power of Two

Solution
Given an integer, write a function to determine if it is a power of two.

Example 1:

```
Input: 1
Output: true 
Explanation: 2^0 = 1
```

Example 2:

```
Input: 16
Output: true
Explanation: 2^4 = 16
```

Example 3:

```
Input: 218
Output: false
```

Solution: 没啥

```
class Solution(object):
    def isPowerOfTwo(self, n):
        """
        :type n: int
        :rtype: bool
        """
        
        if n < 1:
            return False
        
        if n == 1:
            return True
        
        curr_val = 1
        while curr_val < n:
            curr_val = curr_val * 2
            if curr_val == n:
                return True
        return False
```