# Permutation in String

Given two strings s1 and s2, write a function to return true if s2 contains the permutation of s1. In other words, one of the first string's permutations is the substring of the second string.

 

Example 1:

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

Example 2:

```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
``` 

Note:

+ The input strings only contain lower case letters.
+ The length of both given strings is in range [1, 10,000].

Sol1: 

Use Counter for compare

```
from collections import Counter

class Solution(object):
    def checkInclusion(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        N = len(s1)
        ht1 = Counter(s1)
        
        if len(s2) < len(s1):
            return False
        
        ht2 = Counter(s2[:N])
        if ht1 == ht2:
            return True
        
        for i in range(N, len(s2)):
            ht2[s2[i-N]] -= 1
            if ht2[s2[i-N]] == 0:
                del ht2[s2[i-N]]
            
            ht2[s2[i]] += 1
            
            if ht1 == ht2:
                return True
        return False
        
```