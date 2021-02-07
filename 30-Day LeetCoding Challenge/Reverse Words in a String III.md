Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

Example 1:
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
Note: In the string, each word is separated by single space and there will not be any extra space in the string.

Solution 1: simple but very slow

```
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        res = []
        
        i = 0
        while i < len(s):
            if s[i] == ' ':
                i += 1
                continue
            
            j = i + 1
            while j < len(s) and s[j] != ' ':
                j += 1
            res.append(s[i:j][::-1])
            
            i = j
        return ' '.join(res)
```

Sol 2 ~94 with python built-in function

```
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        res = s.split(' ')
        return ' '.join([x[::-1] for x in res])
```
