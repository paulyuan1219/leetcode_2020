# Implement Trie (Prefix Tree)


Implement a trie with insert, search, and startsWith methods.

Example:

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // returns true
trie.search("app");     // returns false
trie.startsWith("app"); // returns true
trie.insert("app");   
trie.search("app");     // returns true
```

Note:

+ You may assume that all inputs are consist of lowercase letters a-z.
+ All inputs are guaranteed to be non-empty strings.


Solution:

很简单，就是开始做的时候不小心，直接用了`ord(c)`来做，造成越界。记住，其实需要用offset，要减去`ord('a')`

```
class Trie(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.flag_end = False
        self.children = [None for x in range(26)]
        

    def insert(self, word):
        """
        Inserts a word into the trie.
        :type word: str
        :rtype: None
        """
        p = self # point to the root
        for i in range(len(word)):
            c = word[i]
            c_code = ord(c) - ord('a')
            
            if p.children[c_code] is None:
                # never see this c_code before
                p.children[c_code] = Trie()
            
            p = p.children[c_code]
            
            if i == len(word) - 1:
                p.flag_end = True


    def search(self, word):
        """
        Returns if the word is in the trie.
        :type word: str
        :rtype: bool
        """
        
        p = self
        
        for c in word:
            c_code = ord(c) - ord('a')
            
            if p.children[c_code] is None:
                return False
            p = p.children[c_code]
        return p.flag_end
        

    def startsWith(self, prefix):
        """
        Returns if there is any word in the trie that starts with the given prefix.
        :type prefix: str
        :rtype: bool
        """
        p = self
        
        for c in prefix:
            c_code = ord(c) - ord('a')
            
            if p.children[c_code] is None:
                return False
            p = p.children[c_code]
        return True
        


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
