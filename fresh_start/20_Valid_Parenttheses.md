```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        
        if len(s) == 0:
            return True
        
        arr = []
        for c in s:
            if c == '(' or c == '[' or c == '{':
                arr.append(c)
            elif c == ')' and (len(arr) > 0 and arr[-1] == '('):
                arr.pop()
            elif c == ']' and (len(arr) > 0 and arr[-1] == '['):
                arr.pop()
            elif c == '}' and (len(arr) > 0 and arr[-1] == '{'):
                arr.pop()
            else:
                return False
        
        if len(arr) == 0:
            return True
        else:
            return False
```
