# Majority Element

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:

```
Input: [3,2,3]
Output: 3
```

Example 2:

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

Solution 1:
use hashtable, but not that fast

```
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ht = {nums[0]:1}
        k = nums[0]
        for num in nums[1:]:
            if len(ht) == 0:
                ht[num] = 1
                k = num
                continue
            else:
                if num in ht:
                    ht[num] += 1
                else:
                    ht[k] -= 1
                    if ht[k] == 0:
                        del ht[k]
        for k in ht:
            return k
```

Solution2 :

不使用hashmap，只用两个数来保存即可

```
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        k = nums[0]
        v = 1
        for num in nums[1:]:
            if v == 0:
                v = 1
                k = num
                continue
            else:
                if num == k:
                    v += 1
                else:
                    v -= 1
        return k
```

精简的写法

```
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        k, v = nums[0], 1
        for num in nums[1:]:
            if v == 0:
                k, v = num, 1
            else:
                v = v + 1 if num == k else v - 1
        return k
```