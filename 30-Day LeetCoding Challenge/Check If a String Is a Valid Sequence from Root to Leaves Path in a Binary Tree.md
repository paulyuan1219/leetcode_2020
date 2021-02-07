# Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree

Given a binary tree where each path going from the root to any leaf form a valid sequence, check if a given string is a valid sequence in such binary tree. 

We get the given string from the concatenation of an array of integers arr and the concatenation of all values of the nodes along a path results in a sequence in the given binary tree.

 

Example 1:


```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,1,0,1]
Output: true
Explanation: 
The path 0 -> 1 -> 0 -> 1 is a valid sequence (green color in the figure). 
Other valid sequences are: 
0 -> 1 -> 1 -> 0 
0 -> 0 -> 0

```

Example 2:

```

Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,0,1]
Output: false 
Explanation: The path 0 -> 0 -> 1 does not exist, therefore it is not even a sequence.

```

Example 3:


```
Input: root = [0,1,0,0,1,0,null,null,1,0,0], arr = [0,1,1]
Output: false
Explanation: The path 0 -> 1 -> 1 is a sequence, but it is not a valid sequence.
```

Constraints:

+ 1 <= arr.length <= 5000
+ 0 <= arr[i] <= 9
+ Each node's value is between [0 - 9].


Solution 1:

我首先按我的想法做，感觉上，只要有一条路走得通，那么就是成功了。后来运行下面这个发现无法通过，原因就在于，这条path的末端必须是一个叶子节点。比如说8所在的这个节点还有孩子，所以8本身并不构成一个valid path，所以无效 醉了 呵呵

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isValidSequence(self, root, arr):
        """
        :type root: TreeNode
        :type arr: List[int]
        :rtype: bool
        """
        def helper(node, curr_str):
            if node is None:
                # we are reaching a empty leaf node now
                return True if len(curr_str) == 0 else False
            elif len(curr_str) == 0:
                return False
            else:
                # now we know that both sides are not empty
                if node.val != curr_str[0]:
                    return False
                else:
                    # node.val == curr_str[0]
                    # we know that this value is correct, now we need to test its children
                    left_result = helper(node.left, curr_str[1:])
                    right_result = helper(node.right, curr_str[1:])
                    return left_result or right_result
        return helper(root, arr)
```

Solution 2:

根据上面的经验，我们修改一下help函数，每次多一个判断，这个是不是叶子节点，就行了 没那么复杂。

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def isValidSequence(self, root, arr):
        """
        :type root: TreeNode
        :type arr: List[int]
        :rtype: bool
        """
        def helper(node, curr_str):
            # here, we must assure that node is a valid node
            
            if len(curr_str) == 0:
                return False 
            
            if node.left is None and node.right is None:
                # this node is a leaf node
                if len(curr_str) == 1 and node.val == curr_str[0]:
                    return True
                else:
                    return False
            else:
                # current node has at least one child, we have to go further
                if node.val != curr_str[0]:
                    return False
                
                left_result, right_result = False, False
                if node.left is not None:
                    left_result = helper(node.left, curr_str[1:])
                if node.right is not None:
                    right_result = helper(node.right, curr_str[1:])
                return left_result or right_result

        return helper(root, arr)
```
 