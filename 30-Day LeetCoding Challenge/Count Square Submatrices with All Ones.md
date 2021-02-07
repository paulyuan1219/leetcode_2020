# Count Square Submatrices with All Ones
Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.

 

Example 1:

```
Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
Explanation: 
There are 10 squares of side 1.
There are 4 squares of side 2.
There is  1 square of side 3.
Total number of squares = 10 + 4 + 1 = 15.
```

Example 2:

```
Input: matrix = 
[
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
Explanation: 
There are 6 squares of side 1.  
There is 1 square of side 2. 
Total number of squares = 6 + 1 = 7.
```

Constraints:

+ 1 <= arr.length <= 300
+ 1 <= arr[0].length <= 300
+ 0 <= arr[i][j] <= 1

Solution 1: DP simple

```
class Solution(object):
    def countSquares(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: int
        """
        M = len(matrix)
        if M == 0:
            return 0
        if M == 1:
            return M[0].sum()
        
        N = len(matrix[0])
        if N == 0:
            return 0
        if N == 1:
            return sum([x[0] for x in matrix])
        
        A = []
        A0 = matrix[0]
        A.append(A0)
        
        for i in range(1, M):
            if matrix[i][0] == 0:
                A.append([0] * N)
            else:
                A.append([1] + [0]*(N-1))
        
        for i in range(1, M):
            for j in range(1, N):
                if matrix[i][j] == 0:
                    A[i][j] = 0
                else:
                    curr_min = min(min(A[i-1][j-1], A[i][j-1]), A[i-1][j])
                    A[i][j] = curr_min + 1
        res = 0
        for row in A:
            res += sum(row)
        return res
                
```
