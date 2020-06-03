# Course Schedule
There are a total of numCourses courses you have to take, labeled from 0 to numCourses-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

 

Example 1:

Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
Example 2:

Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
 

Constraints:

The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
You may assume that there are no duplicate edges in the input prerequisites.
1 <= numCourses <= 10^5

Sol 1: Time exceeded

首先，用了一个最傻的方法，针对每一个v，都做一次dfs，检测是否有圈

```
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """

        def helper(node_id, ht, visited_list):
            if node_id in visited_list:
                return False
            visited_list.append(node_id)

            if node_id not in ht:
                return True
            else:  # this is a start point
                for candidate in ht[node_id]:
                    tmp_res = helper(candidate, ht, visited_list)
                    if not tmp_res:
                        return False
                    visited_list.pop()
                return True

        ht = {}
        for elem in prerequisites:
            if elem[0] not in ht:
                ht[elem[0]] = set()  # this is a set

            ht[elem[0]].add(elem[1])

        print(ht)
        for v in range(numCourses):
            visited_list = []
            tmp_res = helper(v, ht, visited_list)
            if not tmp_res:
                return False

        return True
```

Sol 2: 有点慢 只有20 回头再研究一下 哈哈

仔细想了一下，sol1中的许多计算其实是不必要的，我可以另外用一个pool来保存迄今为止见到过的所有的node。访问过的node就不用再访问了 呵呵呵。成功

```
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """

        def helper(node_id, ht, visited_list, pool):
            if node_id in visited_list:
                return False
            
            visited_list.append(node_id)
            pool.add(node_id)

            if node_id in ht:
                for candidate in ht[node_id]:
                    tmp_res = helper(candidate, ht, visited_list, pool)
                    if not tmp_res:
                        return False
            visited_list.pop()
            return True

        ht = {}
        for elem in prerequisites:
            if elem[0] not in ht:
                ht[elem[0]] = set()  # this is a set

            ht[elem[0]].add(elem[1])

        pool = set()
        for v in range(numCourses):
            if v in pool:
                continue
                
            visited_list = []
            tmp_res = helper(v, ht, visited_list, pool)
            if not tmp_res:
                return False

        return True
```
