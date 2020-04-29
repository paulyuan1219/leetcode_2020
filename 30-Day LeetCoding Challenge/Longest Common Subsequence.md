# Longest Common Subsequence


Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

 

If there is no common subsequence, return 0.

 

Example 1:

```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```

Example 2:

```
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.
```

Example 3:

```
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
``` 

Constraints:

+ 1 <= text1.length <= 1000
+ 1 <= text2.length <= 1000
+ The input strings consist of lowercase English characters only.


Solution 1: 

最经典的dp算法，假设考虑text1[m] and text2[n]

```
if text1[m] == text2[n]:
    res = 1 + lcs(m-1, n-1)
else:
    res = max(lcs(m-1, n), lcs(m,n-1)) 
```
就是在初始化的时候要注意，初始化第一行或者第一列的时候，一旦看到一个1，后面的都是1

```
class Solution(object):
    def longestCommonSubsequence(self, text1, text2):
        """
        :type text1: str
        :type text2: str
        :rtype: int
        """
        M, N = len(text1), len(text2)
        
        A = []
        for i in range(M):
            A.append([0]*N)
        
        # set first row
        # note that when after the first 1, all elems after should be 1
        i = 0
        while i < N:
            if text2[i] == text1[0]:
                break
            i += 1
            
        if i < N:
            for j in range(i, N):
                A[0][j] = 1
        
        i = 0
        while i < M:
            if text1[i] == text2[0]:
                break
            i += 1
            
        if i < M:
            for j in range(i, M):
                A[j][0] = 1

        for i in range(1, M):
            for j in range(1, N):
                if text1[i] == text2[j]:
                    A[i][j] = 1 + A[i-1][j-1]
                else:
                    A[i][j] = max(A[i-1][j], A[i][j-1])
        
        return A[M-1][N-1]
```