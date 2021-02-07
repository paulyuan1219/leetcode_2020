# Flood Fill

An image is represented by a 2-D array of integers, each integer representing the pixel value of the image (from 0 to 65535).

Given a coordinate (sr, sc) representing the starting pixel (row and column) of the flood fill, and a pixel value newColor, "flood fill" the image.

To perform a "flood fill", consider the starting pixel, plus any pixels connected 4-directionally to the starting pixel of the same color as the starting pixel, plus any pixels connected 4-directionally to those pixels (also with the same color as the starting pixel), and so on. Replace the color of all of the aforementioned pixels with the newColor.

At the end, return the modified image.

Example 1:

```
Input: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2

Output: [[2,2,2],[2,2,0],[2,0,1]]

Explanation: 
From the center of the image (with position (sr, sc) = (1, 1)), all pixels connected 
by a path of the same color as the starting pixel are colored with the new color.
Note the bottom corner is not colored 2, because it is not 4-directionally connected
to the starting pixel.
```

Note:

+ The length of image and image[0] will be in the range [1, 50].
+ The given starting pixel will satisfy 0 <= sr < image.length and 0 <= sc < image[0].length.
+ The value of each color in image[i][j] and newColor will be an integer in [0, 65535].


Solution 1:

感觉上就是用bfs来做一遍就可以了，没有难度。

```
class Solution(object):
    def floodFill(self, image, sr, sc, newColor):
        """
        :type image: List[List[int]]
        :type sr: int
        :type sc: int
        :type newColor: int
        :rtype: List[List[int]]
        """
        M = len(image)
        N = len(image[0])
        
        ht_visited = {(sr,sc):1}
        l1 = [(sr,sc)]
        oldColor = image[sr][sc]
        while len(l1) > 0:
            x,y = l1.pop(0)
            # ht_visited[(x,y)] = 1 # flag this as visited 
            
            if x - 1 >=0 and image[x-1][y] == oldColor and (x-1, y) not in ht_visited:
                l1.append((x-1, y))
                ht_visited[(x-1, y)] = 1

            if x + 1 < M and image[x+1][y] == oldColor and (x+1, y) not in ht_visited:
                l1.append((x+1, y))
                ht_visited[(x+1, y)] = 1
                
            if y - 1 >=0 and image[x][y-1] == oldColor and (x, y-1) not in ht_visited:
                l1.append((x, y-1))
                ht_visited[(x, y-1)] = 1

            if y + 1 < N and image[x][y+1] == oldColor and (x, y+1) not in ht_visited:
                l1.append((x, y+1))
                ht_visited[(x, y+1)] = 1
        
        for k in ht_visited:
            image[k[0]][k[1]] = newColor
        return image
```

Same with a helper function

```
class Solution(object):
    def floodFill(self, image, sr, sc, newColor):
        """
        :type image: List[List[int]]
        :type sr: int
        :type sc: int
        :type newColor: int
        :rtype: List[List[int]]
        """
        
        def helper(image, M, N, ht_visited, oldColor, x, y):
            if x >= 0 and x < M and y >=0 and y < N and (x,y) not in ht_visited and image[x][y] == oldColor:
                return True
            return False
        
        
        M = len(image)
        N = len(image[0])
        
        ht_visited = {(sr,sc):1}
        l1 = [(sr,sc)]
        oldColor = image[sr][sc]
        while len(l1) > 0:
            x,y = l1.pop(0)
            # ht_visited[(x,y)] = 1 # flag this as visited 
            
            if helper(image, M, N, ht_visited, oldColor, x-1, y):
                l1.append((x-1, y))
                ht_visited[(x-1, y)] = 1

            if helper(image, M, N, ht_visited, oldColor, x+1, y):
                l1.append((x+1, y))
                ht_visited[(x+1, y)] = 1
                
            if helper(image, M, N, ht_visited, oldColor, x, y-1):
                l1.append((x, y-1))
                ht_visited[(x, y-1)] = 1

            if helper(image, M, N, ht_visited, oldColor, x, y+1):
                l1.append((x, y+1))
                ht_visited[(x, y+1)] = 1
        
        for k in ht_visited:
            image[k[0]][k[1]] = newColor
        return image
        
        
```