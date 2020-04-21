# Construct Binary Search Tree from Preorder Traversal


Return the root node of a binary search tree that matches the given preorder traversal.

(Recall that a binary search tree is a binary tree where for every node, any descendant of node.left has a value < node.val, and any descendant of node.right has a value > node.val.  Also recall that a preorder traversal displays the value of the node first, then traverses node.left, then traverses node.right.)

 

Example 1:

Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]

 

Note: 

1 <= preorder.length <= 100
The values of preorder are distinct.


Solution 1:

貌似很简单。只要写一个helper函数，依次向一个二叉树里面插入即可。因为是preorder，所以这个顺序很好掌握。

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def bstFromPreorder(self, preorder):
        """
        :type preorder: List[int]
        :rtype: TreeNode
        """
        
        def helper(r, val):
            """
            r is the tree root note
            val is the value to be inserted
            """
            
            parent = r
            son = r
            while son is not None:
                if son.val > val:
                    # to insert on the left
                    parent = son
                    son = son.left
                else:
                    # to insert on the right
                    parent = son
                    son = son.right
            # now, son is None
            tmp_node = TreeNode(val)
            if parent.val > val:
                parent.left = tmp_node
            else:
                parent.right = tmp_node
            
                
        
        if len(preorder) == 0:
            return None
        
        root = TreeNode(preorder[0])
        for i in range(1, len(preorder)):
            helper(root, preorder[i])
        return root
```
