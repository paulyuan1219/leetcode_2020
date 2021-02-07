#   Number Complement


Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

 

Example 1:

```
Input: 5
Output: 2
Explanation: The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.
``` 

Example 2:

```
Input: 1
Output: 0
Explanation: The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.
``` 

Note:

* The given integer is guaranteed to fit within the range of a 32-bit signed integer.
* You could assume no leading zero bit in the integer’s binary representation.
* This question is the same as 1009: https://leetcode.com/problems/complement-of-base-10-integer/


Solution 1:

就是除法余数这些 没难度

```
class Solution(object):
    def findComplement(self, num):
        """
        :type num: int
        :rtype: int
        """
        arr1 = []
        while num > 0:
            yu = num % 2
            arr1.append(yu)
            num = int((num-yu)/2)
        
        arr1 = arr1[::-1]
        
        arr2 = []
        for x in arr1:
            if x == 0:
                arr2.append(1)
            else:
                arr2.append(0)
        
        res = 0
        for x in arr2:
            res = res*2 + x
        return res
```