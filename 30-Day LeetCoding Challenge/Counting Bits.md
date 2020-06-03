# Counting Bits
Solution
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example 1:

Input: 2
Output: [0,1,1]
Example 2:

Input: 5
Output: [0,1,1,2,1,2]
Follow up:

+ It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
+ Space complexity should be O(n).
+ Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.


Solution:

一次性完成，关键就是在于寻找pattern，找到以后就简单了 呵呵。

核心其实就是按照2的倍数来变化

+ when i < 2^1, it's [0, 1]
+ when i < 2^2, it's one plus the result of 2^1
+ when i < 2^3, it's one plus the result of 2^2
+ when i < 2^4, it's one plus the result of 2^3

```
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        if num == 0:
            return [0]
        if num == 1:
            return [0,1]
        
        res = [0, 1]
        list_t = []
        t = 2
        while t <= num:
            list_t.append(t)
            t = t*2
        list_t.append(t)
        
        p = 0
        i = 2 # this is current value
        while p < len(list_t) - 1:
            left = list_t[p]
            right = list_t[p+1]
            
            while i >= left and i < right:
                res.append(1 + res[i-left])
                i += 1
                if i > num:
                    break
            p += 1
        return res
```
