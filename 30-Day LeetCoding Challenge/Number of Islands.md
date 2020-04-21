Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

Input:
11110
11010
11000
00000

Output: 1
Example 2:

Input:
11000
11000
00100
00011

Output: 3

Solution 1: 超时

最简单的思路，就是依次遍历，每次看到一个1，就开始调用一个helper函数，把其上下左右所有的1都遍历一遍，同时把所有遍历过的1都改成2.

但是这样居然会超时？想不通

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        def helper(G, M, N, i, j):
            # i,j is valid and G[i,j]==1 and this is the first time we visit this elem
            
            Q = [(i,j)] # start point
            G[i][j] = "2"
            
            while len(Q) > 0:
                x,y = Q.pop(0)
                
                if x-1 >=0 and G[x-1][y] == "1": # the upper side has a valid index
                    G[x-1][y] == "2"
                    Q.append((x-1, y))
                elif x+1 < M and G[x+1][y] == "1":
                    G[x+1][y] == "2"
                    Q.append((x+1, y))
                elif y-1 >=0 and G[x][y-1] == "1":
                    G[x][y-1] == "2"
                    Q.append((x, y-1))
                elif y+1 < N and G[x][y+1] == "1":
                    G[x][y+1] == "2"
                    Q.append((x, y+1))
            return 1
            
        
        M = len(grid)
        if M == 0:
            return 0
        N = len(grid[0])
        if N == 0:
            return 0
        
        res = 0
        
        for i in range(M):
            for j in range(N):
                if grid[i][j] == "1":
                    res += helper(grid, M, N, i, j)
        
        return res
```

测试样例，居然超时
```
[["1","1","1","1","0"],["1","1","0","1","0"],["1","1","0","0","0"],["0","0","0","0","0"]]
```

好吧，仔细检查发现，上面的四个if应该是同时检查的，而不是elif。修改一下，但是还是超时。。。

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        def helper(G, M, N, i, j):
            # i,j is valid and G[i,j]==1 and this is the first time we visit this elem
            
            Q = [(i,j)] # start point
            G[i][j] = "2"
            
            while len(Q) > 0:
                x,y = Q.pop(0)
                
                if x-1 >=0 and G[x-1][y] == "1":
                    G[x-1][y] == "2"
                    Q.append((x-1, y))
                if x+1 < M and G[x+1][y] == "1":
                    G[x+1][y] == "2"
                    Q.append((x+1, y))
                if y-1 >=0 and G[x][y-1] == "1":
                    G[x][y-1] == "2"
                    Q.append((x, y-1))
                if y+1 < N and G[x][y+1] == "1":
                    G[x][y+1] == "2"
                    Q.append((x, y+1))
            return 1
            
        
        M = len(grid)
        if M == 0:
            return 0
        N = len(grid[0])
        if N == 0:
            return 0
        
        res = 0
        
        for i in range(M):
            for j in range(N):
                if grid[i][j] == "1":
                    res += 1 
                    helper(grid, M, N, i, j)
        
        return res
```

汗，仔细的单步调试后，发现="2"居然不起作用。原来为1的元素还是1，这就难怪了 呵呵。

第二天我有空又复盘了一下，发现这么做的确还是有问题，单步调试后，发现只有0,0处的元素改了，别的地方都没改。有意思。



嗯 所以还是另外加一个ht吧 保险一点。下面这个总算work了 呵呵。


```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        def helper(G, M, N, i, j, ht):
            # i,j is valid and G[i,j]==1 and this is the first time we visit this elem
            
            Q = [(i,j)] # start point
            ht[(i,j)] = 1 # mark as visited
            
            while len(Q) > 0:
                x,y = Q.pop(0)
                
                if x-1 >=0 and G[x-1][y] == "1" and (x-1,y) not in ht:
                    ht[(x-1,y)] = 1
                    Q.append((x-1, y))
                if x+1 < M and G[x+1][y] == "1" and (x+1,y) not in ht:
                    ht[(x+1,y)] = 1
                    Q.append((x+1, y))
                if y-1 >=0 and G[x][y-1] == "1" and (x, y-1) not in ht:
                    ht[(x,y-1)] = 1
                    Q.append((x, y-1))
                if y+1 < N and G[x][y+1] == "1" and (x, y+1) not in ht:
                    ht[(x,y+1)] = 1
                    Q.append((x, y+1))
            return 1
            
        
        M = len(grid)
        if M == 0:
            return 0
        N = len(grid[0])
        if N == 0:
            return 0
        
        res = 0
        
        ht = {}
        
        for i in range(M):
            for j in range(N):
                if grid[i][j] == "1" and (i,j) not in ht:
                    res += 1 
                    helper(grid, M, N, i, j, ht)
        
        return res
```

updated on April 18, 2020

我又仔细研究了，使用下面的代码，发现的确在设置为2的时候出了问题。出了0，0被正确设置外，其余的都没有变，所以导致了死循环，有意思。

```
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """

        def helper(G, i, j):
            # i,j is valid and G[i,j]==1 and this is the first time we visit this elem
            Q = [(i, j)]  # start point
            G[i][j] = "2"
            print("{},{} is set to 2".format(i, j))
            print(G)

            while len(Q) > 0:
                x, y = Q.pop(0)

                if x - 1 >= 0 and G[x - 1][y] == "1":
                    G[x - 1][y] == "2"
                    print("{},{} is set to 2".format(x-1, y))
                    print(G)
                    Q.append((x - 1, y))
                if x + 1 < len(G) and G[x + 1][y] == "1":
                    G[x + 1][y] == "2"
                    print("{},{} is set to 2".format(x+1, y))
                    print(G)
                    Q.append((x + 1, y))
                if y - 1 >= 0 and G[x][y - 1] == "1":
                    G[x][y - 1] == "2"
                    print("{},{} is set to 2".format(x, y-1))
                    print(G)
                    Q.append((x, y - 1))
                if y + 1 < N and G[x][y + 1] == "1":
                    G[x][y + 1] == "2"
                    print("{},{} is set to 2".format(x, y+1))
                    print(G)
                    Q.append((x, y + 1))
            return 1

        def helper01(G):
            for i in range(len(G)):
                for j in range(len(G[0])):
                    if G[i][j] == "1":
                        G[i][j] = "y"
        M = len(grid)
        if M == 0:
            return 0
        N = len(grid[0])
        if N == 0:
            return 0

        res = 0

        for i in range(M):
            for j in range(N):
                if grid[i][j] == "1":
                    res += 1
                    helper(grid, i, j)

        return res

    def test01(self, grid):
        def helper(G, i, j):
            if G[i][j] == "1":
                G[i][j] = "111"

        M = len(grid)
        N = len(grid[0])
        for i in range(M):
            for j in range(N):
                helper(grid, i, j)

    def test02(self, L):
        def test02_helper(L1):
            def test02_helper_helper(L2):
                def test02_helper_helper_helper(L3):
                    for i in range(len(L3)):
                        L3[i] = 'wei'
                test02_helper_helper_helper(L2)
            test02_helper_helper(L1)
        test02_helper(L)

    def test03(self, M):
        def test03_helper(M1):
            def test03_helper_helper(M2):
                def test03_helper_helper_helper(M3):
                    for i in range(len(M3)):
                        for j in range(len(M3[0])):
                            if M3[i][j] == "1":
                                M3[i][j] = 'y'
                test03_helper_helper_helper(M2)
            test03_helper_helper(M1)
        test03_helper(M)

if __name__ == "__main__":
    A = [["1","1","1","1","0"],["1","1","0","1","0"],["1","1","0","0","0"],["0","0","0","0","0"]]


    sol = Solution()
    #print(A)
    res = sol.numIslands(A)
#print(A)
#sol.test01(A)

# test one dimention list
#A = [1,2,3,4,5]
#print(A)
#sol.test02(A)
#print(A)

#A = [["1","1","1","1","0"],["1","1","0","1","0"],["1","1","0","0","0"],["0","0","0","0","0"]]
#print(A)
#sol.test03(A)
#print(A)

```

输出如下

```
Connected to pydev debugger (build 192.7142.56)
0,0 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
1,0 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
0,1 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
2,0 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
1,1 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
1,1 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
0,2 is set to 2
[['2', '1', '1', '1', '0'], ['1', '1', '0', '1', '0'], ['1', '1', '0', '0', '0'], ['0', '0', '0', '0', '0']]
```
