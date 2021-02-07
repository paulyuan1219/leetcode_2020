# Plus One

Solution
Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.


Solution 1:

```
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        res = []
        
        i = len(digits) - 1
        carry = 0
        
        while i >= 0:
            if i == len(digits) -1:
                tmp_val = digits[i] + 1
            else:
                tmp_val = digits[i] + carry
            if tmp_val < 10:
                res.insert(0, tmp_val)
                carry = 0
                return digits[:i] + res
            else: # tmp_val == 10
                res.insert(0, 0)
                carry = 1
            
            i -= 1
        if carry == 1:
            res.insert(0, 1)
        
        return res
```        
        
            
        
        
        
    