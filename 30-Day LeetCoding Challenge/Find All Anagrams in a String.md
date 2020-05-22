# Find All Anagrams in a String
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```


Example 2:

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

Solution 1: Time exceeded

我用了最最原始的做法，但是开销有点大 呵呵。

```
class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        
        p_key = ''.join(sorted(p))
        ht = {p_key:1}
        
        N = len(p)
        res = []
        for i in range(0, len(s) -N+1):
            curr_key = ''.join(sorted(s[i:i+N]))
            if curr_key in ht:
                res.append(i)
        return res
```

注意，上面的ht其实没有必要，因为我们最终把p变成了一个key，所以只要比较这个字符串即可，而不需要使用ht。当然，这样做仍然超时了，想办法。


Solution 2: 还是超时

想办法，扫描一次，并且拒绝重复扫描，对吧。

```
from collections import Counter

class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        
        p_key = ''.join(sorted(p))
        ht_p = Counter(p)
        N = len(p)
        res = []
        
        start = 0
        for i in range(0, len(s)):
            if s[i] not in ht_p:
                # we see an outlier, just skip to the next one
                start = i+1 # this is the next possible solution.
                continue
            
            # now, we know that s[i] is in p
            if i-start+1 == N:
                curr_key = ''.join(sorted(s[start:i+1]))
                if curr_key == p_key:
                    res.append(start)
                start += 1
        return res
```

Sol3: 还是超时

```
from collections import Counter

class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        
        ht_p = Counter(p)
        N = len(p)
        res = []
        
        for i in range(0, len(s)-N+1):
            ht = Counter(s[i:i+N])
            if ht == ht_p:
                res.append(i)

        return res
```

Sol4: 通过 但是比较慢

本质上就是比较counter。对s遍历一次，每次遇到一个新元素，就更新一下当前counter 再和p的counter比较即可。

```
from collections import Counter

class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        
        ht_p = Counter(p)
        N = len(p)
        res = []
        
        ht = Counter(s[:N])
        if ht == ht_p:
            res.append(0)

        for i in range(N, len(s)):
            prev_index = i-N
            ht[s[prev_index]] -= 1
            if ht[s[prev_index]] == 0:
                del ht[s[prev_index]]
            
            if s[i] not in ht:
                ht[s[i]] = 1
            else:
                ht[s[i]] += 1
            
            if ht == ht_p:
                res.append(i-N+1)
            

        return res
```

