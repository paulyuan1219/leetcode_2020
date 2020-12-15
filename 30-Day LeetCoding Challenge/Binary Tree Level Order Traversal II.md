# Binary Tree Level Order Traversal II

Solution
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]


Sol1: Simple

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        
        if root is None:
            return []
        
        res = [[root, 0]]
        i = 0
        while i < len(res):
            tmp_node, tmp_level = res[i]
            if tmp_node.left is not None:
                res.append([tmp_node.left, tmp_level + 1])
            
            if tmp_node.right is not None:
                res.append([tmp_node.right, tmp_level + 1])
                
            i += 1
        
        res1 = []
        prev_level = 0
        tmp_res = []
        for i in range(len(res)):
            curr_value = res[i][0].val
            curr_level = res[i][1]
            
            if curr_level == prev_level:
                tmp_res.append(curr_value)
            else:
                res1.insert(0, tmp_res)
                
                tmp_res = [curr_value]
                prev_level = curr_level
        res1.insert(0, tmp_res)

                
        return res1
            
        
```