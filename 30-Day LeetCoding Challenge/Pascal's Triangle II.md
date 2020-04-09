Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

n Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:

Input: 3
Output: [1,3,3,1]
Follow up:

Could you optimize your algorithm to use only O(k) extra space?

Solution 1: 82.79%
The most straightforward way is to iterate over each row and compute each row by sequence

```
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        
        k = rowIndex
        if k == 0:
            return [1]
        elif k == 1:
            return [1,1]
        elif k == 2:
            return [1,2,1]
        
        prev_list = [1,2,1]
        for i in range(3, k+1):
            prev_list = [1] + [prev_list[j]+prev_list[j+1] for j in range(len(prev_list)-1)] + [1]
        return prev_list

```
