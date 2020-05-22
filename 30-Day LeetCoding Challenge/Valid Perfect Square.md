# Valid Perfect Square


Given a positive integer num, write a function which returns True if num is a perfect square else False.

Note: Do not use any built-in library function such as sqrt.

Example 1:

```
Input: 16
Output: true
```

Example 2:

```
Input: 14
Output: false
```

Solution 1:

感觉上用二分法就可以了。第一次做的时候出错了，要注意，helper里面的循环结束以后，此时left==right 还需要再判断一次。

```
class Solution(object):
    def isPerfectSquare(self, num):
        """
        :type num: int
        :rtype: bool
        """
        def helper(target, left, right):
            '''
            target: the target number we are looking at
            left: the smallest number under consideration
            right: the largest number under consideration
            '''
            if left >= right:
                return False
            
            
            while left < right:
                mid = int((left+right)/2)

                if mid**2 == target:
                    return True
                elif mid**2 < target:
                    left = mid + 1
                else:
                    right = mid - 1
            
            # here, we know that left >= right
            return left**2 == target
            
        
        if num < 0:
            return False
        
        if num <= 25:
            if num in {0, 1, 4, 9, 16, 25}:
                return True
            else:
                return False
        
        return helper(num, 1, int(num/2))
        
```