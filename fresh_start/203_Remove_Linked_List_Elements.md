```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        
        dummyHead = ListNode(0, head)
        
        prev = dummyHead
        curr = head
        
        while curr is not None:
            # curr is a valid node, check it
            if curr.val != val:
                prev = curr
            else:
                prev.next = curr.next
            curr = curr.next
        
        return dummyHead.next 
```


Better solution

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def removeElements(self, head, val):
        """
        :type head: ListNode
        :type val: int
        :rtype: ListNode
        """
        
        dummyHead = ListNode(0, head)
        
        prev = dummyHead
        
        while prev.next is not None:
            if prev.next.val != val:
                prev = prev.next
            else:
                prev.next = prev.next.next
        
        return dummyHead.next 
```
