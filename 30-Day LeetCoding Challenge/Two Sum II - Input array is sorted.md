Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

Note:

Your returned answers (both index1 and index2) are not zero-based.
You may assume that each input would have exactly one solution and you may not use the same element twice.
Example:

Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.

Solution:

首先，不考虑sorted信息，可以直接使用hashtable

```
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        ht = {numbers[i]: i for i in range(len(numbers))} 
        
        for i in range(len(numbers)):
            diff = target - numbers[i]
            if diff in ht:
                return i+1, ht[diff]+1
```

Solution 2
Since the list is sorted and there is ganranteed one solution and there’s no duplicated values, we can use a 2 pointer approach.

```
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        
        i, j = 0, len(numbers)-1
        
        while i < j:
            curr_sum = numbers[i]+numbers[j]
            if curr_sum == target:
                return i+1, j+1
            elif curr_sum < target:
                i += 1
            else:
                j -= 1
```
