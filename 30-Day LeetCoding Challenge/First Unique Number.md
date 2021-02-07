# First Unique Number

You have a queue of integers, you need to retrieve the first unique integer in the queue.

Implement the FirstUnique class:

+ FirstUnique(int[] nums) Initializes the object with the numbers in the queue.
+ int showFirstUnique() returns the value of the first unique integer of the queue, and returns -1 if there is no such integer.
+ void add(int value) insert value to the queue.
 

Example 1:

```
Input: 
["FirstUnique","showFirstUnique","add","showFirstUnique","add","showFirstUnique","add","showFirstUnique"]
[[[2,3,5]],[],[5],[],[2],[],[3],[]]
Output: 
[null,2,null,2,null,3,null,-1]

Explanation: 
FirstUnique firstUnique = new FirstUnique([2,3,5]);
firstUnique.showFirstUnique(); // return 2
firstUnique.add(5);            // the queue is now [2,3,5,5]
firstUnique.showFirstUnique(); // return 2
firstUnique.add(2);            // the queue is now [2,3,5,5,2]
firstUnique.showFirstUnique(); // return 3
firstUnique.add(3);            // the queue is now [2,3,5,5,2,3]
firstUnique.showFirstUnique(); // return -1
```

Example 2:

```
Input: 
["FirstUnique","showFirstUnique","add","add","add","add","add","showFirstUnique"]
[[[7,7,7,7,7,7]],[],[7],[3],[3],[7],[17],[]]
Output: 
[null,-1,null,null,null,null,null,17]

Explanation: 
FirstUnique firstUnique = new FirstUnique([7,7,7,7,7,7]);
firstUnique.showFirstUnique(); // return -1
firstUnique.add(7);            // the queue is now [7,7,7,7,7,7,7]
firstUnique.add(3);            // the queue is now [7,7,7,7,7,7,7,3]
firstUnique.add(3);            // the queue is now [7,7,7,7,7,7,7,3,3]
firstUnique.add(7);            // the queue is now [7,7,7,7,7,7,7,3,3,7]
firstUnique.add(17);           // the queue is now [7,7,7,7,7,7,7,3,3,7,17]
firstUnique.showFirstUnique(); // return 17
```

Example 3:

```
Input: 
["FirstUnique","showFirstUnique","add","showFirstUnique"]
[[[809]],[],[809],[]]
Output: 
[null,809,null,-1]

Explanation: 
FirstUnique firstUnique = new FirstUnique([809]);
firstUnique.showFirstUnique(); // return 809
firstUnique.add(809);          // the queue is now [809,809]
firstUnique.showFirstUnique(); // return -1
```
 

Constraints:

+ 1 <= nums.length <= 10^5
+ 1 <= nums[i] <= 10^8
+ 1 <= value <= 10^8
+ At most 50000 calls will be made to showFirstUnique and add.

Solution 1: 超时了

最简单的做法，用一个list来保存nums，另一个list保存nums_uniq。

下面这段代码超时了，即使把最后一个q的更新改成`self.q = [x for x in self.nums if self.ht[x] == 1]` 依旧超时

```
from collections import Counter

class FirstUnique(object):

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.nums = [x for x in nums]
        self.ht = Counter(nums)
        self.q = [x for x in nums if self.ht[x] == 1]# [ x if self.ht[x] == 1 for x in nums] 

        
    def showFirstUnique(self):
        """
        :rtype: int
        """
        if len(self.q) > 0:
            return self.q[0]
        else:
            return -1
        

    def add(self, value):
        """
        :type value: int
        :rtype: None
        """
        self.nums.append(value)
        self.ht[value] += 1
        
        if self.ht[value] == 1:
            # we are adding a new elem
            self.q.append(value)
        else:
            # value has duplicates here, we should remove it if possible
            if value in self.q:
                self.q.remove(value)
        
        
        


# Your FirstUnique object will be instantiated and called as such:
# obj = FirstUnique(nums)
# param_1 = obj.showFirstUnique()
# obj.add(value)
```

Solution 2: 

之前用list，太慢了，还是用hashtable比较靠谱。经过查看答案发现，跟我原来的思路差不错
+ 首先为了快，我们需要把所有的unique value放在一个队列里面。为了快速删除和添加，我使用了一个dummy head和dummy tail。这样保证了这个队列里面至少有一头一尾两个node。
+ 同时我使用了两个hash表，一个hash存放所有的unique value。另一个hash存放所有的duplicated value
+ 然后就依次读取一个nums中的每一个值了。
    + 如果这个值 in ht_dup，说明这个值在此之前已经见过至少两次了，当前见到的是第三次或者以上。这种就直接忽略
    + else if value not in ht, 说明这个值从来没见过，现在是第一次见，所以我们可以把它加入ht，同时插入到queue的末尾，也就是dummy tail之前即可。注意，再加入ht的时候，需要同时保存这个新add listnode的地址。这样是为了以后可以快速定位这个node并进行删除
    + else 说明我们是第二次见到这个value，所以我们应当把它从queue里面删除，然后从ht里面删除，再加入ht_dup

```
class ListNode(object):
    def __init__(self, value):
        self.value = value
        self.prev = None
        self.next = None
    
    def add(self, value):
        # this is always called from the dummy tail node
        # a new node is created and inserted just before this dummy tail node
        # notice that after insertion, the dummy tail node doesn't change at all, therefore no return values is needed here.
        tmpnode = ListNode(value)
        
        leftnode = self.prev
        rightnode = self
        
        leftnode.next = tmpnode
        tmpnode.prev = leftnode
        
        tmpnode.next = rightnode
        rightnode.prev = tmpnode
        
    def remove(self):
        # remove current node
        # notice that after removal, the dummy head and dummy tail don't change, so we don't need to return any value here
        
        leftnode = self.prev
        rightnode = self.next
        
        leftnode.next = rightnode
        rightnode.prev = leftnode
      
class FirstUnique(object):

    def __init__(self, nums):
        """
        :type nums: List[int]
        """
        self.head = ListNode("headnode") # points to the dummy head of the list
        self.tail = ListNode("tailnode")
        self.head.next = self.tail
        self.tail.prev = self.head
        
        self.ht_dup = {} # a set containing all duplicates, i.e. a value >=2
        self.ht_freq = {} # saving (value, freq), by default, freq is always 1, when it reaches 2, this key is removed and then added into ht_dup
        
        for num in nums:
            if num in self.ht_dup:
                continue
            
            if num not in self.ht_freq:
                self.tail.add(num)
                self.ht_freq[num] = self.tail.prev # map to the location of the listnode
            else:
                self.ht_freq[num].remove()
                del self.ht_freq[num]
                self.ht_dup[num] = 2
       
    def showFirstUnique(self):
        """
        :rtype: int
        """
        
        if self.head.next == self.tail:
            return -1
        else:
            return self.head.next.value

    def add(self, value):
        """
        :type value: int
        :rtype: None
        """
        num = value
        if num in self.ht_dup:
            return

        if num not in self.ht_freq:
            self.tail.add(num)
            self.ht_freq[num] = self.tail.prev # map to the location of the listnode
        else:
            self.ht_freq[num].remove()
            del self.ht_freq[num]
            self.ht_dup[num] = 2

        
        
        


# Your FirstUnique object will be instantiated and called as such:
# obj = FirstUnique(nums)
# param_1 = obj.showFirstUnique()
# obj.add(value)
```

