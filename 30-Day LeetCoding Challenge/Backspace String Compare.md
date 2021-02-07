Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.

Example 1:

Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
Example 2:

Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
Example 3:

Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
Example 4:

Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
Note:

1 <= S.length <= 200
1 <= T.length <= 200
S and T only contain lowercase letters and '#' characters.
Follow up:

Can you solve it in O(N) time and O(1) space?

Solution 1: 

Just use 2 stacks to compute final strings. 

```
class Solution(object):
    def backspaceCompare(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: bool
        """
        
        def helper(s):
            l = []
            for char in s:
                if char != '#':
                    l.append(char)
                elif len(l) > 0:
                    l.pop()
            return ''.join(l)
        
        S_str = helper(S)
        T_str = helper(T)
        
        return S_str == T_str
```
Solution 2.

Use no extra space

```
class Solution(object):
    def backspaceCompare(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: bool
        """
        
        ps = len(S) - 1
        pt = len(T) - 1
        
        ssharp = 0
        tsharp = 0
        
        while True:
            while ps >=0:
                if S[ps] == '#':
                    ssharp += 1
                    ps -= 1
                elif ssharp > 0:
                    ssharp -= 1
                    ps -= 1
                else:
                    break
            # now, ps < 0 or S[ps] is a valid ending char
            
            while pt >=0:
                if T[pt] == '#':
                    tsharp += 1
                    pt -= 1
                elif tsharp > 0:
                    tsharp -= 1
                    pt -= 1
                else:
                    break
            # now, pt < 0 or T[pt] is a valid ending char
            
            if ps >=0 and pt >=0:
                if S[ps] != T[pt]:
                    return False
                else:
                    ps -= 1
                    pt -= 1
            elif ps < 0 and pt < 0:
                return True
            else:
                return False
 ```       
