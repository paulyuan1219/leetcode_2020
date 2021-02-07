# Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example:

Input: 

```
1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0
```

Output: 4

Solution 1: Error

第一个想到的就是用dp来做。基本的想法就是拉一个对角线，从左上到右下。每当evaluate一个位置的时候，我们只要检查其左上，左，上这三个方向上的当前最大square的边长，即可。

但是这里有一点小trick。一开始我只是希望这三个数都大于零。后来发现不对，因为都大于零不能保证当前检查的两条边上没有零。所以重新定义了下面这个，但是还不对，因为太严格了，漏掉了很多。所以仔细想一想，假设有一个子square的边长是n。那么在最后这个位置，我们需要检查三个邻居：左，左上，上。对着三个邻居来说，每一个都应当是square且边长为n-1，这样，才能保证最后一个位置的square的边长是n。

再仔细想一想，只要在三个邻居的边长中取最小值，然后+1即可 呵呵。

```
class Solution(object):
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        
        M = len(matrix)
        if M == 0:
            return 0
        
        N = len(matrix[0])
        if N == 0:
            return 0
        
        A = []
        for i in range(M):
            A.append([0]*N)
        
        res = 0
        for i in range(M):
            if matrix[i][0] == "1":
                A[i][0] = 1
                res = 1
        
        for j in range(N):
            if matrix[0][j] == "1":
                A[0][j] = 1
                res = 1
        
        for i in range(1, M):
            for j in range(1, N):
                if matrix[i][j] == "0":
                    A[i][j] = 0
                    continue
                
                curr_value = 1
                if A[i-1][j-1] > 0 and A[i][j-1] >= A[i-1][j-1] and A[i-1][j] >= A[i-1][j-1]:
                    curr_value = 1 + A[i-1][j-1]
                
                A[i][j] = curr_value
                if res < curr_value:
                    res = curr_value
        return res**2
                
```

Solution 2: Perfect

```
class Solution(object):
    def maximalSquare(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        
        M = len(matrix)
        if M == 0:
            return 0
        
        N = len(matrix[0])
        if N == 0:
            return 0
        
        A = []
        for i in range(M):
            A.append([0]*N)
        
        res = 0
        for i in range(M):
            if matrix[i][0] == "1":
                A[i][0] = 1
                res = 1
        
        for j in range(N):
            if matrix[0][j] == "1":
                A[0][j] = 1
                res = 1
        
        for i in range(1, M):
            for j in range(1, N):
                if matrix[i][j] == "0":
                    A[i][j] = 0
                    continue
                
                curr_min = min(A[i-1][j-1], min(A[i][j-1], A[i-1][j]))
                if curr_min == 0:
                    A[i][j] = 1
                else:
                    A[i][j] = 1+curr_min
                if res < A[i][j]:
                    res = A[i][j]
        return res**2
                
        
```        