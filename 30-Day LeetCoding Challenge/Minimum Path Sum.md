Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.


Solution 1:

第一感觉就是，这个是用动态规划来做。

如果原始输入只是一行或者一列，那么直接求和即可。

否则的话，就先把第一行和第一列搞定，然后一行一行依次扫描，反正每一次到一个新的位置，要么是从上面下来的，要么是从左边过来的，很简单。

```
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        M = len(grid)
        if M == 0:
            return 0
        
        N = len(grid[0])
        if N == 0:
            return 0
        
        # now, we know there are >=1 elem in the matrix
        if M == 1:
            return sum(grid[0])
        
        if N == 1:
            return sum([row[0] for row in grid])
        
        # now, it's a normal matrix, use DP
        A = []
        for i in range(M):
            A.append([0] * N)
        
        tmp_sum = 0
        for i in range(N):
            tmp_sum += grid[0][i]
            A[0][i] = tmp_sum
        
        tmp_sum = 0
        for i in range(M):
            tmp_sum += grid[i][0]
            A[i][0] = tmp_sum
        
        for i in range(1, M):
            for j in range(1, N):
                A[i][j] = min(A[i-1][j], A[i][j-1]) + grid[i][j]
        
        return A[-1][-1]
```