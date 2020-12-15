# Island Perimeter

Solution
You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.

 

Example:

Input:
[[0,1,0,0],
 [1,1,1,0],
 [0,1,0,0],
 [1,1,0,0]]

Output: 16

Explanation: The perimeter is the 16 yellow stripes in the image below:

Solution 1:
Simple, just need to iterate over each position and count number of edges. That's it.

```
class Solution(object):
    def islandPerimeter(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        def get_local_perimeter(i, j, grid):
            M = len(grid)
            N = len(grid[0])
            
            if grid[i][j] == 0:
                return 0
            
            res = 0
            # check up
            if i == 0 or grid[i-1][j] == 0:
                res += 1
            
            # check down
            if i == M-1 or grid[i+1][j] == 0:
                res += 1
            
            # check left
            if j == 0 or grid[i][j-1] == 0:
                res += 1
            
            # check right
            if j == N-1 or grid[i][j+1] == 0:
                res += 1
            
            return res
        
        M = len(grid)
        N = len(grid[0])
        res = 0
        for i in range(M):
            for j in range(N):
                res += get_local_perimeter(i, j, grid)
        return res
    
            
            

```