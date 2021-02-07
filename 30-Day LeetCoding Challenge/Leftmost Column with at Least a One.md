# Leftmost Column with at Least a One

(This problem is an interactive problem.)

A binary matrix means that all elements are 0 or 1. For each individual row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least a 1 in it. If such index doesn't exist, return -1.

You can't access the Binary Matrix directly.  You may only access the matrix using a BinaryMatrix interface:

BinaryMatrix.get(x, y) returns the element of the matrix at index (x, y) (0-indexed).
BinaryMatrix.dimensions() returns a list of 2 elements [n, m], which means the matrix is n * m.
Submissions making more than 1000 calls to BinaryMatrix.get will be judged Wrong Answer.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix mat as input in the following four examples. You will not have access the binary matrix directly.

 

Example 1:



Input: mat = [[0,0],[1,1]]
Output: 0
Example 2:



Input: mat = [[0,0],[0,1]]
Output: 1
Example 3:



Input: mat = [[0,0],[0,0]]
Output: -1
Example 4:



Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
 

Constraints:

1 <= mat.length, mat[i].length <= 100
mat[i][j] is either 0 or 1.
mat[i] is sorted in a non-decreasing way.

Solution:

最开始的想法就是先找到第一个含有1的行，这样就可以得到当前行的最左边的1的位置。

然后可以依次扫描接下来的每一行。对于每一个新的行，只需要检查从0到当前leftmost位置的元素即可，如果有1，那么说明当前行的leftmost更小，需要更新这个值。否则，就直接忽略这一行即可。

在写完以上函数之后，发现，其实可以就把默认的返回值开到最大，就是n，即矩阵的列数。然后我们一次扫描每一行即可，没那么复杂。


```
# """
# This is BinaryMatrix's API interface.
# You should not implement it, or speculate about its implementation
# """
#class BinaryMatrix(object):
#    def get(self, x, y):
#        """
#        :type x : int, y : int
#        :rtype int
#        """
#
#    def dimensions:
#        """
#        :rtype list[]
#        """

class Solution(object):
    def leftMostColumnWithOne(self, binaryMatrix):
        """
        :type binaryMatrix: BinaryMatrix
        :rtype: int
        """
        
        def helper(M, i, prev_left):
            '''
            Now we are looking at M[i]
            prev_left is the current leftmost index of 1, so far
            for example, suppose previous row is [0,0,1,1,1]
            Then prev_left = 2
            For current row, we only need to check M[i][:prev_left], to see if there is a one
            
            Note, if prev_left == n, this means previous row is all zeros
            '''
            
            p1 = 0
            p2 = prev_left-1
            while p1 < p2:
                mid = int((p1+p2)/2)
                
                if M.get(i, mid) == 1:
                    p2 = mid
                else:
                    p1 = mid + 1
            
            if M.get(i, p1) == 1:
                return p1
            else:
                return prev_left
            
        # first, find the first row which contains at least one 1
        m, n = binaryMatrix.dimensions()
        
        i = 0
        left_index = n # initial value
        while i < m:
            left_index = helper(binaryMatrix, i, left_index)
            if left_index == 0:
                return 0
            i +=1
        return -1 if left_index == n else left_index
```