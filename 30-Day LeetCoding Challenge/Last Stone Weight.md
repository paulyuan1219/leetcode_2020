We have a collection of stones, each stone has a positive integer weight.

Each turn, we choose the two heaviest stones and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:

If x == y, both stones are totally destroyed;
If x != y, the stone of weight x is totally destroyed, and the stone of weight y has new weight y-x.
At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)

 

Example 1:

Input: [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of last stone.
 

Note:

1 <= stones.length <= 30
1 <= stones[i] <= 1000

Solution 1 ~ 93

This is most straightforward way

```
class Solution(object):
    def lastStoneWeight(self, stones):
        """
        :type stones: List[int]
        :rtype: int
        """
        l1 = stones
        
        if len(l1) == 0:
            return 0
        elif len(l1) == 1:
            return l1[0]
        
        while len(l1) >= 2:
            l1 = sorted(l1)
            diff = l1[-1] - l1[-2]
            l1 = l1[:-2]
            if diff > 0:
                l1.append(diff)
        
        if len(l1) == 0:
            return 0
        else:
            return l1[0]
                
```

Solution 2: not finished yet

I should use a heap to maintain the best order. I can either implement the heap, or just use the exising heapq module

```
'''
class Heap(object):
    def __init__(self, stones):
        self.heap = [0] # by doing so, we know stones[1] is the largest one, and his sons are i*2+1
        
        self.heap = [0] + stones
        
        for i in range(2, len(self.heap)):
            self.heapify(i)
        
    def append(self, stone):
        self.heap.append(stone)
        
        self.heapify(len(self.heap)-1)
    
    def pop(self):
        N = len(self.heap)
        
        if N < 2:
            return -1
        
        res = self.heap[1]
        
    def heapify(self, i):
        # [i] is the index of last appended element
        # heap[1:i] (i.e. heap[1], heap[2],...heap[i-1]) is already a heap
        # the minimam possible value of i is 2
        
        if i < 2:
            return
        
        parent_index = int(i/2)
        while parent_index >=1 and self.heap[parent_index] < self.heap[i]:
            self.heap[parent_index], self.heap[i] = self.heap[i], self.heap[parent_index]
            i = parent_index
            parent_index = int(i/2)
        return
    
    def check_consistency(self):
        N = len(self.heap)
        
        if N < 2:
            return
        
        start = 1
        left_child = start*2
        right_child = start*2+1
        
        while left_child < N and right_child < N:
'''            ```

