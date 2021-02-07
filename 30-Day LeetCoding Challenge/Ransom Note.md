# Ransom Note

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

Note:
You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

Solution: 

就是用一个hashtable，很简单

```
from collections import Counter

class Solution(object):
    def canConstruct(self, ransomNote, magazine):
        """
        :type ransomNote: str
        :type magazine: str
        :rtype: bool
        """
        ht = Counter(magazine)
        
        for c in ransomNote:
            if c not in ht:
                return False
            
            ht[c] -= 1
            if ht[c] == 0:
                del ht[c]
        return True
```