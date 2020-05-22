# Cousins in Binary Tree

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

 

Example 1:


Input: root = [1,2,3,4], x = 4, y = 3
Output: false
Example 2:


Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
Example 3:



Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false
 

Note:

The number of nodes in the tree will be between 2 and 100.
Each node has a unique integer value from 1 to 100.


Solution 1:
因为需要depth相同 所以感觉上只要使用bfs即可，用递归，每一次都把当前的depth的所有元素扫一遍，看看是不是x y都在里面。

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isCousins(self, root, x, y):
        """
        :type root: TreeNode
        :type x: int
        :type y: int
        :rtype: bool
        """
        def bfs(q, x, y):
            # q is a list of nodes of the same depth
            # for each elem, we should also save its parent
            if len(q) == 0:
                return False
            
            b_x, b_y = False, False
            p_x, p_y = None, None
            q_new = []
            for elem in q:
                if elem[0].val == x:
                    b_x = True
                    p_x = elem[1]
                elif elem[0].val == y:
                    b_y = True
                    p_y = elem[1]
                else:
                    #it's not x nor y, we have to explore it
                    if elem[0].left is not None:
                        q_new.append((elem[0].left, elem[0]))
                    if elem[0].right is not None:
                        q_new.append((elem[0].right, elem[0]))
            
            if b_x and b_y:
                if p_x == p_y:
                    return False
                else:
                    return True
            elif b_x or b_y:
                return False
            else:
                return bfs(q_new, x, y)
        
        return bfs([(root, None)], x, y)
```
