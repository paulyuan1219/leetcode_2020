# Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

Example 1:

```
Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

Example 2:

```
Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```

Solution 1: 超时。

最直接的做法，用一个list q来保存经过上一步index，可以访问到的所有位置的集合。然后依次pop出q中的第一个index，然后根据这个index本身的value以及nums[index]来计算出从当前index出发可以reach的新的index集合，并把这个新的index集合merge到q中，以此类推。

逻辑上应该是对的，但是每次列表操作，似乎复杂度太高了。

```
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) == 0 or len(nums) == 1:
            return True
        
        N = len(nums)
        
        i = 0
        q = list(range(1, nums[i]+1))
        if N-1 in q:
            return True
        
        while len(q) > 0:
            i = q.pop(0) # i is current index
            #tmp_q = list(range(i+1, i+1+nums[i]))
            for j in range(i+1, i+1+nums[i]):
                if N-1 == j:
                    return True
                else:
                    if j not in q:
                        q.append(j)
        
        return False
```

Solution 2: 完美

仔细想一想，因为限定的是最大步数，所以0到最大步数之间都可以取值，换一句话来说，我们可以用一个上下界来界定当前可以到达的位置。进一步想，下界总是为0，只需要不断更新上界即可。只要上界>=N-1，那么就算成功了 呵呵。

```
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums) == 0 or len(nums) == 1:
            return True
        
        N = len(nums)
        
        
        l = 0
        r = nums[0]
        offset = 0
        
        if r == 0:
            return False
        
        if r >= N -1:
            return True
        
        offset = 1
        while offset <= r:
            # now l+offset is valid, where l is always 0
            curr_r = offset + nums[offset]
            r = max(r, curr_r)
            if r >= N-1:
                return True
            offset += 1
        return False
```
             
             