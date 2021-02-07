
Given an integer array arr, count element x such that x + 1 is also in arr.

If there're duplicates in arr, count them seperately.

 

Example 1:

Input: arr = [1,2,3]
Output: 2
Explanation: 1 and 2 are counted cause 2 and 3 are in arr.
Example 2:

Input: arr = [1,1,3,3,5,5,7,7]
Output: 0
Explanation: No numbers are counted, cause there's no 2, 4, 6, or 8 in arr.
Example 3:

Input: arr = [1,3,2,3,5,0]
Output: 3
Explanation: 0, 1 and 2 are counted cause 1, 2 and 3 are in arr.
Example 4:

Input: arr = [1,1,2,2]
Output: 2
Explanation: Two 1s are counted cause 2 is in arr.
 

Constraints:

1 <= arr.length <= 1000
0 <= arr[i] <= 1000

Solution:

As long as I sort it, then I can iterate this list. Alternatively, we can use a hashtable to save {x-->x_count}. Below we show a one line code to do this.

```
class Solution(object):
    def countElements(self, arr):
        """
        :type arr: List[int]
        :rtype: int
        """
        res = 0
        
        l = sorted(arr)
        curr_key = l[0]
        curr_key_count = 1        
        for elem in l[1:]:
            if curr_key == elem:
                curr_key_count += 1
            else:
                if curr_key + 1 == elem:
                    res += curr_key_count
                curr_key = elem
                curr_key_count = 1
        return res
```


```
class Solution:
    def countElements(self, arr: List[int]) -> int:
        C = collections.Counter(arr)
        return sum(C[x] for x in C if x+1 in C)
```
