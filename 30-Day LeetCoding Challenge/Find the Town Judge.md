# Find the Town Judge


In a town, there are N people labelled from 1 to N.  There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

The town judge trusts nobody.
Everybody (except for the town judge) trusts the town judge.
There is exactly one person that satisfies properties 1 and 2.
You are given trust, an array of pairs trust[i] = [a, b] representing that the person labelled a trusts the person labelled b.

If the town judge exists and can be identified, return the label of the town judge.  Otherwise, return -1.

 

Example 1:

Input: N = 2, trust = [[1,2]]
Output: 2
Example 2:

Input: N = 3, trust = [[1,3],[2,3]]
Output: 3
Example 3:

Input: N = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
Example 4:

Input: N = 3, trust = [[1,2],[2,3]]
Output: -1
Example 5:

Input: N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3
 

Note:

+ 1 <= N <= 1000
+ trust.length <= 10000
+ trust[i] are all different
+ trust[i][0] != trust[i][1]
+ 1 <= trust[i][0], trust[i][1] <= N

Solution 1:

题目本身很简单，只是要注意输入是空串是怎么样，同时还要注意出现重复的时候怎么办 。

```
class Solution(object):
    def findJudge(self, N, trust):
        """
        :type N: int
        :type trust: List[List[int]]
        :rtype: int
        """
        
        if len(trust) == 0:
            return 1
    
        ht = {}
        ht_nonjudge = {} # saving all elem which cannot be the judge
        
        for x in trust:
            if x[1] not in ht:
                ht[x[1]] = []
            ht[x[1]].append(x[0])
            
            ht_nonjudge[x[0]] = 1
        
        
        ht_res = {}
        for k,v in ht.items():
            if len(v) == N-1 and k not in ht_nonjudge:
                ht_res[k] = 1
        
        if len(ht_res) == 1:
            for k in ht_res:
                return k
        else:
            return -1
    
```