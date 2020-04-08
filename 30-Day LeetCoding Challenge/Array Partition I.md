Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), ..., (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.

Example 1:
Input: [1,4,3,2]

Output: 4
Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).
Note:
n is a positive integer, which is in the range of [1, 10000].
All the integers in the array will be in the range of [-10000, 10000].

Solution:

The basic idea is that min(x,y) is dominated by the smaller value. If x << y, then the power of y is wasted. In other words, we should keep x,y similar as possible as we can. <br>

This leads to a natual sorting algorithm. We just sort the array, and then sum up one every two elements.

```
class Solution(object):
    def arrayPairSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums1 = sorted(nums)
        return sum([nums1[i] for i in range(0, len(nums), 2)])
```

Solution 2:

This time, we use a hash table. The code is short . The time complexity is high, only beating 7%

```
class Solution(object):
    def arrayPairSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        offset = 10000
        freq_array = [0] * 20001
        for num in nums:
            freq_array[num+offset] += 1

        l = []
        for i in range(len(freq_array)):
            if freq_array[i] > 0:
                l.extend([i-offset for x in range(freq_array[i])])
                if len(l) == len(nums):
                    break
        return sum([l[i] for i in range(0, len(l), 2)])
```

Solution 3: 比2还要差。。。

```
class Solution(object):
    def arrayPairSum(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        offset = 10000
        freq_array = [0 for x in range(offset*2+1)]# [0] * 20001
        for num in nums:
            freq_array[num+offset] += 1

        N = int(len(nums)/2) # this our target number of completed pairs
        res = [] # a list of min values of each pair
        pair_middle = False
        for i in range(len(freq_array)):
            if freq_array[i] > 0:
                curr_value = i - offset
                curr_freq = freq_array[i]
                if pair_middle:
                    curr_freq -= 1
                    pair_middle = False
                
                if curr_freq == 0:
                    continue
                
                if curr_freq%2 == 0:
                    times = int(curr_freq / 2)
                else:
                    times = int(curr_freq / 2) + 1
                    pair_middle = True
                res += [curr_value for x in range(times)]
                
                if len(res) == N:
                    return sum(res)
        return -1
```
