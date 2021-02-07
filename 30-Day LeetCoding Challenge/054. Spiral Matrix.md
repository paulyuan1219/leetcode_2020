Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

Example 1:

Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
Example 2:

Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]

Solution:

备注，这个题目本身不算很难，但是边界的检测方面比较tricky，我开始的时候大意了，是看了test case失败的时候才发现哪里出了问题，呵呵。

首先，感觉我们可以用递归来做，每一层递归就是做一圈，分为向右向下向左向上，这样就是一圈。然后只要记录圈数就可以了。

在一开始的时候，在绕一圈的时候，使用了左闭右开的方式，就是向右的时候，从零开始，最后剩下一个。然后向下，也是从零开始，最后剩下一个。然后向左，也是从tail开始往左，到1结束。然后是向上，从最后一行开始，向上，还是剩下最后一个。这样四个方向都跑完一圈，就是一个loop 然后我们loop count ++, 再继续做下一轮。

注意，when lc is a int in [0, 1,2,...]，说明我们已经跑完了lc圈，那么再下一次做的时候，我们的开始位置其实是 (lc, lc)。所以我们只需要做一下几个方向
```
            res1 = matrix[lc][lc:N - lc] # we are at row-lc
            res2 = [x[N-1-lc] for x in matrix[lc+1: M -1 - lc]] # we are at col-(N-1-lc)
            res3 = matrix[M-1-lc][lc:N-lc][::-1] if M-1-lc != lc else []
            res4 = [x[lc] for x in matrix[1+lc:M-lc-1]][::-1] if N-1-lc != lc else []
```
注意，这里我使用的是水平方向到底，垂直方向相应缩短的写法。之所以不用之前说的左闭右开的方式，是因为它无法处理最后剩下单个元素未曾访问的情况，比如example 1中间的5

这里
注意，这里我使用的是水平方向到底，垂直方向相应缩短的写法。之所以不用之前说的左闭右开的方式，是因为它无法处理最后剩下单个元素未曾访问的情况，比如example 1中间的5的
注意，这里我使用的是水平方向到底，垂直方向相应缩短的写法。之所以不用之前说的左闭右开的方式，是因为它无法处理最后剩下单个元素未曾访问的情况，比如example 1中间的5

注意，如果只是这么写的话，上述的5有可能被访问两次，就是水平方向向右一次，向左再一次，垂直方向没有。为了解决这个问题，我们在计算res3 res4的时候，必须保证res3和res1不重叠，res4和res2不重叠

还有一点很需要注意，在一个测试case中，我们出了错，对于一个shape=(2,10)的矩阵，我们的结果多跑了很多。仔细查看以后，发现我们在程序的入口处还需要一个验证。对于给定的matrix以及固定的M N，我们当遇到一个新的lc的时候，必须看看此时我们将要访问的还是不是一个合理的矩阵。换句话说，如果发现下一个矩阵里面已经被访问过了，那么就应该及时返回。


```
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        def helper(matrix, M, N, lc): # lc means loop count, default = 0
            # first, need to validate
            if lc > M-1-lc or lc > N-1-lc:
                return []
            
            res1 = matrix[lc][lc:N - lc] # we are at row-lc
            res2 = [x[N-1-lc] for x in matrix[lc+1: M -1 - lc]] # we are at col-(N-1-lc)
            res3 = matrix[M-1-lc][lc:N-lc][::-1] if M-1-lc != lc else []
            res4 = [x[lc] for x in matrix[1+lc:M-lc-1]][::-1] if N-1-lc != lc else []
            
            res = res1 + res2 + res3 + res4
            if len(res1) == 0 or len(res2) == 0 or len(res3) == 0 or len(res4) == 0:
                return res
            else:
                # they are all non-zero, which means we can go another loop
                return res + helper(matrix, M, N, lc+1)
            
       
        M = len(matrix)
        if M == 0:
            return []
        N = len(matrix[0])
        if N == 0:
            return []
        if M == 1:
            return matrix[0]
        if N == 1:
            return [x[0] for x in matrix]
        
        # if we reach here, the matrix is a normal one, with num_rows >=2 and num_cols >=2
        # Therefore, we can have at least one loop
        return helper(matrix, M, N, 0)
```
