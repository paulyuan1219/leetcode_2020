# Check If It Is a Straight Line

You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

```
Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
Output: true
```

```
Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
Output: false
```

Constraints:

+ 2 <= coordinates.length <= 1000
+ coordinates[i].length == 2
+ -10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4
+ coordinates contains no duplicate point.

Solution 1:

Just check slope, should be easy

```
class Solution(object):
    def checkStraightLine(self, coordinates):
        """
        :type coordinates: List[List[int]]
        :rtype: bool
        """
        
        point0 = coordinates[0]
        point1 = coordinates[1]
        
        if point0[0] == point1[0]:
            # we have a vertical line
            for i in range(2, len(coordinates)):
                if coordinates[i][0] != point0[0]:
                    return False
            return True
        elif point0[1] == point1[1]:
            # we have a horizontal line
            for i in range(2, len(coordinates)):
                if coordinates[i][1] != point0[1]:
                    return False
            return True
        else:
            # it's a normal line with valid slope
            slope = float((point1[1]-point0[1])/(point1[0]-point0[0]))
            
            for i in range(2, len(coordinates)):
                if coordinates[i][0] == point0[0]:
                    return False
                
                curr_slope = float((coordinates[i][1]-point0[1])/(coordinates[i][0]-point0[0]))
                
                if abs(curr_slope - slope) > 1e-7:
                    return False
            return True
        

```

奇怪，为啥说我不对呢

```
Submission Result: Wrong Answer 
Input:
[[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
Output:
true
Expected:
false
```

好吧 是整数的除法出错了。应该改成浮点数的除法。

```
                curr_slope = float((coordinates[i][1]-point0[1]))/(coordinates[i][0]-point0[0])

```