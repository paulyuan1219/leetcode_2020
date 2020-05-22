# Kth Smallest Element in a BST


Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Example 1:

Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
Example 2:

Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
Follow up:
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?


Sol1:

第一次做的时候犯了错，只是返回一个当前的offset 或者是val，这个有点混了。现在用一个list的引用来做，貌似更简单。

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def kthSmallest(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: int
        """
        
        def midorder(node, k, res):
            if node is None:
                return
            
            midorder(node.left, k, res)
            
            if len(res) < k:
                res.append(node.val)
            
            if len(res) == k:
                return
            else:
                midorder(node.right, k, res)
        res = []
        midorder(root, k, res)
        return res[-1]
```