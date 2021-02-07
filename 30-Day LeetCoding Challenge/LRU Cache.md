# LRU Cache

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

Follow up:
Could you do both operations in O(1) time complexity?

Example:

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```

Solution 1:

最简单的做法，用一个ht来保存所有的kv对，这样保证常数时间的访问。同时用一个LRU队列。每次更新的时候使得最新被访问的key放到队尾即可。就是时间复杂度有点高。

```
class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.ht = {}
        self.q = []
        self.capacity = capacity
        

    def get(self, key):
        """
        :type key: int
        :rtype: int
        """
        
        if key not in self.ht:
            return -1
        
        i = self.q.index(key)
        self.q.pop(i)
        self.q.append(key)
        
        return self.ht[key]
        

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: None
        """
        
        # first, check if key already exists. If so , just override it
        if key in self.ht:
            self.ht[key] = value
            i = self.q.index(key)
            self.q.pop(i)
            self.q.append(key)
            return
    
        # not we see a new key
        if len(self.ht) < self.capacity:
            self.ht[key] = value
            self.q.append(key)
        else:
            old_key = self.q.pop(0)
            # del self.ht[old_key]
            self.ht.pop(old_key, None)
            
            self.ht[key] = value
            self.q.append(key)
        


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)

```

好吧 看了官方答案，一个使用了python的一个orderdict，算是作弊。另一个用了一个额外的双向列表，醉了。
