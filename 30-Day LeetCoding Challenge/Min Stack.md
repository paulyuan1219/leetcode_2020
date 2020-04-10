Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
 

Example:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.

Solution 1 after reading hint

```
class MinStack(object):

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.arr = []
        

    def push(self, x):
        """
        :type x: int
        :rtype: None
        """
        if len(self.arr) == 0:
            self.arr.append((x, x))
        else:
            curr_min = self.arr[-1][1]
            self.arr.append((x, min(x, curr_min)))
        

    def pop(self):
        """
        :rtype: None
        """
        self.arr.pop()
        
        

    def top(self):
        """
        :rtype: int
        """
        if len(self.arr) > 0:
            return self.arr[-1][0]
        else:
            return -1
        

    def getMin(self):
        """
        :rtype: int
        """
        if len(self.arr) > 0:
            return self.arr[-1][1]
        else:
            return -1
        


# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```
