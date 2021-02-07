# Leetcode 2021



### 485. Max Consecutive Ones

Sol 1: (2020-01-16)

This is my first attempt. It works, but is very slow.

The basic idea is to find the first 1, then find the first 0 after it. Then compute current length.

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        
        if len(nums) == 1:
            if nums[0] == 0:
                return 0
            else:
                return 1
        
        # now we have len(nums) >=2
        prev_i = -1
        i = 0
        res = 0
        
        while True:
            # skip leading 0s
            while i < len(nums) and nums[i] == 0:
                i += 1
            
            if i == len(nums): # we know the last elem is 0
                return res
            
            # now, we know that nums[i] is the first 1 we ever see
            prev_i = i
            
            # Now, search for the first seen 1
            i = i +1
            
            while i < len(nums) and nums[i] == 1:
                i += 1
            
            # here, we know that i == len(nums) or nums[i] == 0
            # In either case, i is one position ahead of the 1 string
            tmp_res = i - prev_i
            res = max(res, tmp_res)
            
            if i == len(nums):
                return res
            
            # Move to the next part
            prev_i = i
            i = i + 1
        
```

Sol 2: (2020-01-16)

This is what I have seen after checking the official guide

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        count = 0
        
        for num in nums:
            if num == 1:
                count += 1
            else:
                res = max(res, count)
                count = 0
        return max(res, count)
```

Sol 3: (2020-01-16)

This is an improvement of Sol 2

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        count = 0
        
        for num in nums:
            if num == 1:
                count += 1
            else:
                if count > 0:
                    res = max(res, count)
                    count = 0
        return max(res, count)
```

Here's the best solution

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        res = 0
        count = 0
        
        for num in nums:
            if num == 1:
                count += 1
            elif count > 0:
                res = max(res, count)
                count = 0
        return max(res, count)
```



### 1295. Find Numbers with Even Number of Digits

Sol 1: (2020-01-16)

```
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        res = 0
        
        for num in nums:
            if len(str(num)) % 2 == 0:
                res += 1
        return res
```





### Squares of a Sorted Array

Sol 1: (2020-01-16)

```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        if len(nums) == 0:
            return []
        elif nums[0] >= 0:
            # all nums are >=0
            return [x*x for x in nums]
        elif nums[-1] <= 0:
            # all nums are <= 0
            return [x*x for x in nums[::-1]]
        
        # here, we know that some nums are < 0 and some nums are > 0
        # try to find the first num >= 0
        i = 0
        while i < len(nums) and nums[i] < 0:
            i += 1
        
        p1 = i
        p2 = i-1
        
        res = []
        
        while p1 < len(nums) and p2 >=0:
            if nums[p1] <= -nums[p2]:
                res.append(nums[p1] * nums[p1])
                p1 += 1
            else:
                res.append(nums[p2] * nums[p2])
                p2 -= 1
        
        if p1 < len(nums):
            res += [x*x for x in nums[p1:]]
        
        if p2 >= 0:
            res += [x*x for x in nums[:p2+1][::-1]]
        
        return res

```







Sol 1: (2020-01-16)

基本思路是这样，

首先从左往右便利，同时计算新的arr的大小。一旦超过N就停止，因为新的arr的长度还是N

此时，原来的arr的长度为N

而原来arr[:i]扩展后的长度为n

当n==N的时候，最简单。从右往左一个个计算就可以

当n==N+1的时候，最后一个元素其实是0，需要单独处理即可。

```
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        N = len(arr)
        
        n = 0

        i = 0
        while i < N:
            if arr[i] != 0:
                n += 1
            else:
                n += 2
            
            # n is the number in the new arr list
            if n >= N:
                break
            
            i += 1
        
        if n == N:
            # this means the new arr list len is exact. good to know
            j = N - 1
            while i >= 0:
                if arr[i] != 0: # just one bit
                    arr[j] = arr[i]
                    j -= 1
                    i -= 1
                else: # we need 2 bits
                    arr[j] = 0
                    arr[j-1] = 0
                    
                    j -= 2
                    i -= 1
            return
        elif n == N + 1:
            # this means the last elem is 0, we just need to keep one of it
            arr[-1] = 0
            
            i -= 1
            j = N-2
            while i >= 0:
                if arr[i] != 0: # just one bit
                    arr[j] = arr[i]
                    j -= 1
                    i -= 1
                else: # we need 2 bits
                    arr[j] = 0
                    arr[j-1] = 0
                    
                    j -= 2
                    i -= 1
            return            

```



以上可以进一步简化一下，效果也很好

```
class Solution:
    def duplicateZeros(self, arr: List[int]) -> None:
        """
        Do not return anything, modify arr in-place instead.
        """
        N = len(arr)
        
        n = 0

        i = 0
        while i < N:
            if arr[i] != 0:
                n += 1
            else:
                n += 2
            
            # n is the number in the new arr list
            if n >= N:
                break
            
            i += 1
        
        if n == N:
            # this means the new arr list len is exact. good to know
            j = N - 1
        else:
            arr[-1] = 0
            
            i -= 1
            j = N-2
            
        while i >= 0:
            if arr[i] != 0: # just one bit
                arr[j] = arr[i]
                j -= 1
                i -= 1
            else: # we need 2 bits
                arr[j] = 0
                arr[j-1] = 0

                j -= 2
                i -= 1
        return
```



### Merge Sorted Array

Sol 1: (2020-01-16)

同时维护nums1的尾部指针 以及nums2的尾部指针，然后依次比较即可

速度很慢，不知太确定为什么

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        
        p = m + n -1 # this is the last available slot in nums1
        
        i = m-1 # last non-empty elem in nums1
        j = n-1 # last non-empty elem in nums2
        
        while i >= 0 and j >=0:
            if nums1[i] <= nums2[j]:
                nums1[p] = nums2[j]
                j -= 1
            else:
                nums1[p] = nums1[i]
                i -= 1
            
            p -= 1
        
        if j < 0:
            return
        else:
            nums1[:j+1] = nums2[:j+1]
            return
```



### Remove Element

Sol 1: (2020-01-16) 效率还算可以 呵呵

基本思路

首先，先find第一个val出现的位置。如果没有，则trivial

其次，在上面位置后面寻找第一个nonval 如果没有，则trivial

把上面这两个位置的元素交换，然后继续。这一步很tricky，不能够nums[i] = nums[j] 这样就会更改了arr里面的原始信息 不对了，要注意



```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        if len(nums) == 0:
            return
        
        N = len(nums)
        
        # try to find the first occurrence of val
        i = 0
        while i < N and nums[i] != val:
            i += 1

        if i == N:
            return N # in this case, we cannot find val in nums
        
        # Here, we know the first val, let's find the first non-val after it
        j = i + 1
        while j < N and nums[j] == val:
            j += 1
        if j == N:
            return i
        nums[i], nums[j] = nums[j], nums[i]
        
        i += 1
        j += 1
        
        while True:
            while i < N and nums[i] != val:
                i += 1

            if i == N:
                return N # in this case, we cannot find val in nums
            
            # here, we know that nums[i] is the first item == val
            j = max(j, i+1)
            while j < N and nums[j] == val:
                j += 1
            
            if j == N:
                # in this case, everything from nums[i] are the same, all equal to val
                return i
            
            # here, nums[j] is the first elem <> val
            nums[i], nums[j] = nums[j], nums[i]
            
            i += 1
            j += 1
```

Sol 2: (2020-01-17)

做了几道题，有点感觉了。其实和Move Zeros那个很像，基本是一样的做法

```
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        N = len(nums)
        
        i = 0
        
        for j in range(N):
            if nums[j] == val:
                continue
            else:
                if i == j:
                    i += 1
                else:
                    nums[i] = nums[j]
                    i += 1
        
        return i
```





### Remove Duplicates from Sorted Array

Sol1: (2020-01-16)

居然没有pass，不要慌 呵呵

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        def findFirstVal(nums, index_start):
            """
            Try to find the first duplicate pairs from nums[index_start], if not found, return -1
            """
            i = index_start
            
            while i < len(nums) -1 and nums[i] != nums[i+1]:
                i += 1
            
            if i == len(nums) -1:
                # we are at the end, and there's no duplicate pairs found
                return -1
            else:
                return i+1
        
        def findFirstNonval(nums, index_start, target):
            """
            In nums[index_start:], find the first elem which is > target
            """
            
            i = index_start
            
            while i < len(nums) and nums[i] <= target:
                i += 1
            
            if i == len(nums):
                return -1
            else:
                # we find it
                return i
            
            
        N = len(nums)
        
        if N < 2:
            return N

        pos1 = findFirstVal(nums, 0)
        
        if pos1 < 0:
            return 1
        
        # here, nums[pos] == nums[pos-1], we should update pos's elem
        pos2 = findFirstNonval(nums, pos1+1, nums[pos1])
        
        if pos2 < 0:
            return pos1
        
        #here, we know that we find the next available stuff
        nums[pos1] = nums[pos2]
        
        pos1 = pos1 + 1
        target = nums[pos2]
        pos2 = pos2 + 1
        
        while True:
            pos1_new = findFirstVal(nums, pos1)

            if pos1_new < 0:
                return pos1

            pos2_new = findFirstNonval(nums, pos1_new+1, nums[pos1_new])

            if pos2_new < 0:
                return pos1_new

            nums[pos1_new] = nums[pos2_new]

            pos1 = pos1_new + 1
            target = nums[pos2_new]
            pos2 = pos2_new + 1  
```

Sol 2: (2020-01-17)

还是不对 醉了

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N < 2:
            return N
        
        i = 0
        i_val = nums[i]
        j = 1
        last_val = nums[i] # this is the last elem in the new array
        
        while True:
            old_i = i
            while i < N -1 and nums[i] != nums[i+1]:
                last_val = nums[i]
                i += 1
            
            if i == N-1:
                return old_i + 1
            
            # if reach here, we know that nums[i] == nums[i+1]
            
            first_slot = i+1
            
            # start to move j
            j = max(first_slot+1, j)
            while j < N and nums[j] <= last_val:
                j += 1
            
            if j == N:
                return i+1
            
            # find it
            nums[first_slot] = nums[j]
            last_val = nums[j]
            
            i += 1
            j += 1
            
```

Sol 3 2020-01-17 看了官方解答

这个很简洁，而且有个好处，每次更新以后，nums[i]里面就是新array里面的最后一个elem，所以里面的判断语句只需要用不等式就可以了，厉害啊 哈哈。

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N < 2:
            return N
        

        i = 0
        for j in range(1, N):
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]
        return i+1
```





### Check If N and Its Double Exist

Sol 1 (2020-01-17)

简单debug了一下，主要问题在于，1）重复元素的处理 2）0的处理，别的没啥，就是用ht即可



```
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        ht = {}
        for i in range(len(arr)):
            if arr[i] not in ht:
                ht[arr[i]] = 1 
            else:
                ht[arr[i]] += 1
        
        for i in range(len(arr)):
            target = 2 * arr[i]
            
            if target in ht:
                if target == 0:
                    if ht[target] > 1:
                        return True
                else:
                    return True
        return False
```



### Valid Mountain Array

Sol 1: (2020-01-17)

自己做的，有一个小bug 就是当整个arr都是下降的时候，忘记处理了，所以说边际要很小心



```
class Solution:
    def validMountainArray(self, arr: List[int]) -> bool:
        N = len(arr)
        
        if N < 3:
            return False
        
        
        # check first part
        i = 0
        while i < N -1 and arr[i] < arr[i+1]:
            i += 1
        
        if i == 0:
            return False
        
        if i == N -1:
            return False
        
        while i < N - 1 and arr[i] > arr[i+1]:
            i += 1
        
        if i == N-1:
            return True
        else:
            return False
```



### Replace Elements with Greatest Element on Right Side

Sol 1: (2020-01-17)



直观上不是很难。只要从右往左扫描一遍即可。然后把扫描的结果输出即可。

```
class Solution:
    def replaceElements(self, arr: List[int]) -> List[int]:
        N = len(arr)
        
        if N == 0:
            return []
        
        if N == 1:
            return [-1]
        
        arr2 = [0 for x in arr]
        arr2[-1] = arr[-1]
        
        tmp_max = arr[-1]
        for i in range(N-2, -1, -1):
            tmp_max = max(tmp_max, arr[i])
            arr2[i] = tmp_max
        
        return arr2[1:] + [-1]
```





### Remove Duplicates from Sorted Array

Sol 1: (2020-01-17)

比较简单。使用两个指针。第一个指针始终指向即将插入的位置，第二个指针寻找下一个不等于零的位置。然后赋值即可。

注意，最后需要把剩下的位置全部清零。

```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        
        N = len(nums)
        
        if N == 0:
            return
        
        i = 0
        
        for j in range(N):
            if nums[j] == 0:
                continue
            else:
                if i == j:
                    i += 1
                else:
                    nums[i] = nums[j]
                    i += 1
        
        for k in range(i, N):
            nums[k] = 0
        
```



### Sort Array By Parity

Sol 1: (2020-01-17)

直接in place即可，双指针 向中间移动 并交换



```
class Solution:
    def sortArrayByParity(self, A: List[int]) -> List[int]:
        N = len(A)
        
        if N < 2:
            return A
        
        i = 0
        j = N -1 
        
        while i < j:
            while i < j and A[i]%2==0:
                i += 1
            
            if i == j:
                break
            
            # now, A[i] is an odd number
            
            while j > i and A[j]%2 == 1:
                j -= 1
            
            if j == i:
                break
            
            # Now, A[j] is even
            
            A[i], A[j] = A[j], A[i]
            
            i += 1
            j -= 1
        return A
```











首先把最简单的情况单独处理，然后就是找到中间的分界点，然后分别做即可。但是效率似乎不太高

```
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        if len(nums) == 0:
            return []
        elif nums[0] >= 0:
            # all nums are >=0
            return [x*x for x in nums]
        elif nums[-1] <= 0:
            # all nums are <= 0
            return [x*x for x in nums[::-1]]
        
        # here, we know that some nums are < 0 and some nums are > 0
        # try to find the first num >= 0
        i = 0
        while i < len(nums) and nums[i] < 0:
            i += 1
        
        p1 = i
        p2 = i-1
        
        res = []
        
        while p1 < len(nums) and p2 >=0:
            if nums[p1] <= -nums[p2]:
                res.append(nums[p1] * nums[p1])
                p1 += 1
            else:
                res.append(nums[p2] * nums[p2])
                p2 -= 1
        
        if p1 < len(nums):
            res += [x*x for x in nums[p1:]]
        
        if p2 >= 0:
            res += [x*x for x in nums[:p2+1][::-1]]
        
        return res

```



### Find All Numbers Disappeared in an Array

Sol 1: (2020-01-17)

基本思路很简单，新建一个array，然后用每个数字的序号作为index

看起来就像一个binary vector

```
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        N = len(nums)
        
        res = [0 for x in nums] + [0]
        
        for num in nums:
            res[num] = 1
        
        res2 = []
        for i in range(1, N+1):
            if res[i] == 0:
                res2.append(i)
        return res2
```

### Height Checker

Sol 1: (2020-01-17)

这个题目很low，看了别人的答案才看出来，没啥意思

```
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        sorted_heights = sorted(heights)
        summ = 0
        for i in range(len(heights)) :
            if heights[i] != sorted_heights[i] :
                summ += 1
        return summ        
```

### Max Consecutive Ones II

Sol 1: (2020-01-17) not successful

我开始就用给自己的直觉来做，貌似很复杂

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        old_ones = 0
        new_ones = 0
        zeros_in_between = 0
        
        
        res = 0
        for num in nums:
            if num == 1:
                if prev_zero:
                    prev_zero = False
                    placeholder = 1
                else:
                    prev_one = True
                new_ones += 1
                
            else:
                if prev_one:
                    # then this is the first zero afterwards
```

Sol 2: (2020-01-18)

根据官方解答，整理一下思路。

首先，最暴力的方法当然是全部都检查。

首先，left = 0, then right = 0, 1, 2, 3 依次向右遍历，同时计算[left, right]区间内0的个数。一旦0的个数超过1，那么这个区间就invalid，就是不可能再有更长得了。

然后left++，即left=1, then right = 1, 2, 3...思路同上

然后left++，即left=2, then right = 2, 3...思路同上

总结，我们考虑left在每个位置的可能性。首先固定left，然后不断向右扩展right。也就是说，针对left可能处在的每一个位置，我们都考虑从left开始向右最多能扩展到多少。

所以理论上，是$O(N^2)$的复杂性

接下来，我们来看看当前有哪些是可以改进的。

假设固定了left，那么向右的这个阶段已经是最右的了。显然，我们必须向右一个一个元素的看过去，中间不能跳过，对吧。一旦发现有两个0了，那么显然，从当前left开始就只能够走那么远了，所以及时停止，没有问题。

所以问题好像在于，我们似乎可以更好的更新left。比如说，给定序列100001。那么刚刚开始left=0, right=0 OK, right=1 OK, right=2 Bad 此时[left, right]=100 里面的0超过了，所以无效。此时如果我们执行left++ 那么left=1 and arr[left] = 0，我们再从right=1,2,3这么一个个看过来。但是根据刚刚无效的那段，我们已经知道了right=2 and arr[right]=0 所以我们其实可以把上面的无用功给去掉。换句话说，我们需要把left继续向右移动，知道当前[left, right]里面最多只有一个0位置。这样的话，我们可以更快速的移动left，从而降低整个的复杂度，没错吧，就是这样。

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N == 0:
            return 0
        elif N == 1:
            return 1
        
        left = 0
        right = left
        zero_count = 0
        
        longest_seq = 0
        
        # Note, nums[left:right+1] is a valid string, with at most 1 zero in between.
        # Anytime, the subarray above is well maintained
        for right in range(N):
            if nums[right] == 1:
                longest_seq = max(longest_seq, right - left + 1)
            else:
                zero_count += 1
                if zero_count >= 2:
                    # if so, we know that there are more than 2 zeros in the subarray, have to move left to shink it
                    while zero_count >= 2:
                        if nums[left] == 0:
                            zero_count -= 1
                        left += 1
        
        return longest_seq
```

注意，上面的代码有问题，因为longest_seq只有在遇到一个1的时候才会更新，否则就一直为0。所以，当input里面全部都是0的时候，返回值也是0，但是期望输出是1.要注意。

下面的代码通过了 呵呵

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N == 0:
            return 0
        elif N == 1:
            return 1
        
        left = 0
        right = left
        zero_count = 0
        
        longest_seq = 0
        
        # Note, nums[left:right+1] is a valid string, with at most 1 zero in between.
        # Anytime, the subarray above is well maintained
        for right in range(N):
            if nums[right] == 1:
                longest_seq = max(longest_seq, right - left + 1)
            else:
                zero_count += 1
                
                if zero_count == 1:
                    # we only have 1 zero in [left, right], we can still count it
                    longest_seq = max(longest_seq, right - left + 1)
                elif zero_count >= 2:
                    # if so, we know that there are more than 2 zeros in the subarray, have to move left to shink it
                    while zero_count >= 2:
                        if nums[left] == 0:
                            zero_count -= 1
                        left += 1
        
        return longest_seq
            
```

仔细想一想，貌似可以更加精简

```
class Solution:
    def findMaxConsecutiveOnes(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N == 0:
            return 0
        elif N == 1:
            return 1
        
        left = 0
        right = left
        zero_count = 0
        
        longest_seq = 0
        
        # Note, nums[left:right+1] is a valid string, with at most 1 zero in between.
        # Anytime, the subarray above is well maintained
        for right in range(N):
            if nums[right] == 0:
                zero_count += 1
            
            if zero_count <= 1:
                longest_seq = max(longest_seq, right - left + 1)
            else:
                # if so, we know that there are more than 2 zeros in the subarray, have to move left to shink it
                while zero_count >= 2:
                    if nums[left] == 0:
                        zero_count -= 1
                    left += 1
        
        return longest_seq
```



### Third Maximum Number

Sol 1: (2020-01-18)

使用python现有的sort set，没啥难度 呵呵 复杂度主要在于sorted 


$$
O(nLogn)
$$


```
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        arr = sorted(list(set(nums)))
        
        if len(arr) >= 3:
            return arr[-3]
        else:
            return arr[-1]
```

Sol 2: (2020-01-18)

维持三个数字 a b c 然后线性扫描即可。

理论上说应该是线性的，但是实际过程中超时了，不太好

```
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N == 1:
            return nums[0]
        elif N == 2:
            return max(nums[0], nums[1])
        
        a = nums[0]
        
        i = 1
        while i < N and nums[i] == a:
            i += 1
        
        if i == N:
            # in this case, all elems in nums are the same
            return a
        
        # in this case, we find the first nums[i] which is different than a
        b = nums[i]
        
        if a > b:
            a, b = b, a
        
        j = i + 1
        while j < N and (nums[j] == a or nums[j] == b):
            j += 1
        
        if j == N:
            return b
        
        c = nums[j] # by default
        
        if c < a:
            c = b
            b = a
            a = nums[j]
        elif c < b:
            b, c = c, b
        
        # here, we have a < b < c
        k = j + 1
        while k < N and (nums[k] != a and nums[k] != b and nums[k] != c):
            if nums[k] < a:
                continue
            elif nums[k] < b:
                a = nums[k]
            elif nums[k] < c:
                a, b = b, nums[k]
            else: # nums[k] > c
                a = b
                b = c
                c = nums[k]
        
        return a

```



稍微修改了一下，还是超时

```
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        N = len(nums)
        
        if N == 1:
            return nums[0]
        elif N == 2:
            return max(nums[0], nums[1])
        
        a = nums[0]
        
        i = 1
        while i < N and nums[i] == a:
            i += 1
        
        if i == N:
            # in this case, all elems in nums are the same
            return a
        
        # in this case, we find the first nums[i] which is different than a
        b = nums[i]
        
        if a > b:
            a, b = b, a
        
        j = i + 1
        while j < N and (nums[j] == a or nums[j] == b):
            j += 1
        
        if j == N:
            return b
        
        c = nums[j] # by default
        
        if c < a:
            c = b
            b = a
            a = nums[j]
        elif c < b:
            b, c = c, b
        
        # here, we have a < b < c
        k = j + 1
        while k < N:
            if nums[k] < a:
                continue
            elif nums[k] > a and nums[k] < b:
                a = nums[k]
            elif nums[k] > b and nums[k] < c:
                a, b = b, nums[k]
            elif nums[k] > c:
                a = b
                b = c
                c = nums[k]
        
        return a

```

好吧，看了一下官方解答，我的思路是对的，只是具体的实现上，他们使用了本身的set，所以显得简单一点，醉了。

下面这个官方解答跟我的想法是一样的，只是用了set而已

```
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        max_set = set()
        
        for num in nums:
            max_set.add(num)
            if len(max_set) > 3:
                max_set.remove(min(max_set))
        
        if len(max_set) == 3:
            return min(max_set)
        else:
            return max(max_set)
```

### Design Linked List

Sol 1: (2020-01-18)

这个就是很直接的做，没有做任何的优化，只是用了一个dummyhead来方便处理，没啥

```
class MyLinkedList:
    class ListNode:
        def __init__(self, val):
            self.val = val
            self.next = None
        
        def __init__(self, val, next):
            self.val = val
            self.next = Next
        
        
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.dummyHead = ListNode(0)
        

    def get(self, index: int) -> int:
        """
        Get the value of the index-th node in the linked list. If the index is invalid, return -1.
        """
        
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode.next is not None:
            # here, we know that tmpNode.next is a valid node, just check its index
            if i == index:
                # this is the one we want to search
                return tmpNode.next.val
            else:
                i += 1
                tmpNode = tmpNode.next
        
        # if here, there is no such node
        return -1
            
        

    def addAtHead(self, val: int) -> None:
        """
        Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
        """
        tmpNode = ListNode(val, self.dummyHead.next)
        self.dummyHead.next = tmpNode
        

    def addAtTail(self, val: int) -> None:
        """
        Append a node of value val to the last element of the linked list.
        """
        
        tmpNode = self.dummyHead
        
        while tmpNode.next is not None:
            tmpNode = tmpNode.next
        
        tmpNode.next = ListNode(val)
        

    def addAtIndex(self, index: int, val: int) -> None:
        """
        Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
        """
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode is not None:
            if i == index:
                # this is the right place
                newNode = ListNode(val, tmpNode.next)
                tmpNode.next = newNode
                return
            else:
                i += 1
                tmpNode = tmpNode.next
        
        return
        
        

    def deleteAtIndex(self, index: int) -> None:
        """
        Delete the index-th node in the linked list, if the index is valid.
        """
        
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode is not None and tmpNode.next is not None:
            if i == index:
                tmpNode.next = tmpNode.next.next
                return
            else:
                i += 1
                tmpNode = tmpNode.next
        return
            
        


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```



### Linked List Cycle

Sol 1: (2020-01-18)

这道题目之前做过，用两个指针就可以了，只是原理好像还不清楚，不管了 先写吧



```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        """ 下面这部分可以去掉 不影响
        if head is None:
            return False
        elif head.next is None:
            return False
        elif head.next == head:
            return True
        """
        # Now we know there are >=2 nodes
        slow = head
        fast = head
        
        while True:
            if slow is None or fast is None:
                return False
            
            slow = slow.next
            
            if fast.next is None:
                return False
            else:
                fast = fast.next.next
            
            if slow == fast:
                return True
```



好吧，网上找到了一个简单的解答，说的通

> https://zhenye-na.github.io/2018/09/03/linkedlist-cycle-ii.html
>
> 一开始使用了复杂度 O(n2)O(n2)的方法，使用两个指针a, b。a从表头开始一步一步往前走，遇到null则说明没有环，返回 `false` ；a每走一步，b从头开始走，如果遇到 `b==a.next` ，则说明有环 `true` ，如果遇到 `b==a` ，则说明暂时没有环，继续循环。
>
> 后来找到了复杂度O(n)的方法，使用两个指针slow,fast。两个指针都从表头开始走，slow每次走一步，fast每次走两步，如果fast遇到null，则说明没有环，返回false；如果 `slow==fast`，说明有环，并且此时fast超了slow一圈，返回true。
>
> 为什么有环的情况下二者一定会相遇呢？**因为fast先进入环，在slow进入之后，如果把slow看作在前面，fast在后面每次循环都向slow靠近1，所以一定会相遇，而不会出现fast直接跳过slow的情况**。



### Linked List Cycle II

Sol 1: (2020-01-18)

这道题目之前做过，用两个指针就可以了，其实就是上面的延续。

首先，利用上面的方式，如果没有环，很简单，直接返回即可。如果有，那么重新开始两个比赛，一个人从head出发，每次走一步，另一个人从meeting point出发，每次也走一个。这样，两个人的新的汇合点就是环开始的地方。

举个例子，假设第一次汇合的时候，slow走了n1+n2的距离，其中
$$
distance(head-->cycle-entry) = n1 \\
distance(cycle-entry-->meeting point) = n2\\

distance(meeting point-->cycle-entry) = n3
$$
显然，在第一次汇合点上，slow走过了n1+n2 ， fast走过了 n1 + n2 + n3 + n2 。又因为fast走的路程是slow的一倍，所以有2(n1+n2) = n1 + n2 + n3 + n2 ==> n1 = n3。

所以，由于我们需要知道的是n1的val，所以只要重新从head走一遍即可。

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        slow = head
        fast = head
        
        while True:
            if slow is None or fast is None or fast.next is None:
                return None
            
            slow = slow.next
            fast = fast.next.next
            
            if slow == fast:
                # they meet
                slow = head
                
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                
                return slow
            
```



### Intersection of Two Linked Lists

Sol 1: (2020-01-18)

使用自带的ht来做，这样最快，不过没有难度

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        ht = set()
        tmpnode = headA
        while tmpnode is not None:
            ht.add(tmpnode)
            tmpnode = tmpnode.next
            
        tmpnode = headB
        while tmpnode is not None:
            if tmpnode in ht:
                return tmpnode
            tmpnode = tmpnode.next
        
        return None
```

Sol 2: (2020-01-18)

以前做过，用头尾相连来做。推导也比较容易

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        
        p1 = headA
        p1_round = 1
        p2 = headB
        p2_round = 1
        
        if p1 is None or p2 is None:
            return None
        
        while True:
            if p1 == p2:
                return p1
            
            p1 = p1.next
            p2 = p2.next
            
            if p1 is None:
                # we are at the end of a list
                if p1_round == 1:
                    p1_round = 2
                    p1 = headB
                else:
                    return None
            
            if p2 is None:
                if p2_round == 1:
                    p2_round = 2
                    p2 = headA
                else:
                    return None
```



### Remove Nth Node From End of List

Sol 1: (2021-01-18)

首先，可以先跑一遍，求出N，然后走n步即可，方法如下

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummyHead = ListNode(0, head)
        
        N = 0
        tmpNode = dummyHead.next
        while tmpNode is not None:
            N += 1
            tmpNode = tmpNode.next
        
        if n < 1 or n > N:
            return None
        
        endNode = dummyHead
        for i in range(n):
            endNode = endNode.next
        
        beginNode = dummyHead
        
        while endNode.next is not None:
            endNode = endNode.next
            beginNode = beginNode.next
        
        beginNode.next = beginNode.next.next
        return dummyHead.next
```

但是仔细想一想，上面的N其实也没啥用 完全可以去掉 哈哈

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummyHead = ListNode(0, head)
        
        endNode = dummyHead
        for i in range(n):
            endNode = endNode.next
            if endNode is None:
                # this means that the input is invalid
                return None
        
        beginNode = dummyHead
        
        while endNode.next is not None:
            endNode = endNode.next
            beginNode = beginNode.next
        
        beginNode.next = beginNode.next.next
        return dummyHead.next
```



### Reverse Linked List

Sol 1: (2020-01-19)

这个解答其实是看过之前第一章的介绍的，直接用一个循环即可，概念上来看很容易

以下这个是采用iteratively的方法

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
            return head
        
        # here, we know that len(list) >= 2
        p1 = head
        p2 = p1.next
        newhead = p1
        
        while p2 is not None:
            p1.next = p2.next
            p2.next = newhead
            newhead = p2
            
            p2 = p1.next
        
        return newhead
```

Sol 2: (2020-01-19)

Recursive method

注意，第一次coding的时候反了错误，居然忘记吧末尾node的next设置为空了。造成了死循环 呵呵

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
            return head
        
        # here, we know that len(list) >= 2
        def f1(h):
            if h.next is None:
                return (h, h)
            else:
                n1 = h
                b, e = f1(h.next)
                e.next = n1
                n1.next = None # This line is important
                
                return b, n1
        
        newhead, newtail = f1(head)
        return newhead

```

### Remove Linked List Elements

Sol 1: (2020-01-19)

没啥难度，trivial

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummyHead = ListNode(0, head)
        
        p = dummyHead
        while p.next is not None:
            if p.next.val == val:
                p.next = p.next.next
            else:
                p = p.next
        
        return dummyHead.next
```

### Odd Even Linked List

Sol 1: (2020-01-19)

好像也没啥，写一个循环即可，首先处理len <=1 的情况，然后设置两个头部指针，分别处理即可，没啥

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if head is None or head.next is None:
            return head
        
        # Here, we know len(list) >= 2
        h1 = head
        h2 = head.next
        
        p1 = h1
        p2 = h2
        
        while True:
            if p2.next is not None and p2.next.next is not None:
                p1.next = p2.next
                p2.next = p2.next.next
                
                p1 = p1.next
                p2 = p2.next
            elif p2.next is not None and p2.next.next is None:
                p1.next = p2.next
                p2.next = None
                
                p1.next.next = h2
                return h1
            else:
                # p2.next is None
                p1.next = h2
                return h1
```

### Palindrome Linked List

Sol 1: (2020-01-19)

其实就是从左往右 和从右往左遍历都一样。

首先，把linked list转化成字符串，然后逆序比较，很容易，只是这样空间太大，打不到O(1)的要求

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        arr1 = []
        p = head
        while p is not None:
            arr1.append(p.val)
            p = p.next
        
        arr2 = arr1[::-1]
        
        return arr1 == arr2
```

> Could you do it in O(n) time and O(1) space?

想一想应该怎么做呢 呵呵？

一个直观的想法是使用快慢指针，第一次遍历先找到中间节点，然后从中间节点开始，把后半段逆序排列，如果这个list是满足题目要求的，那么前半段和后半段的逆序应该一样 哈哈，就这么定了。

下面这个一次性通过 不错不错

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if head is None or head.next is None:
            return True
        
        def f1(h):
            # reverse a list with head h
            if h.next is None:
                return (h, h)
            else:
                n1 = h
                b, e = f1(h.next)
                e.next = n1
                n1.next = None
                
                return (b, n1)
                
        dummyHead = ListNode(0, head)
        
        p1 = dummyHead
        p2 = dummyHead
        
        while True:
            p1 = p1.next
            p2 = p2.next.next
            
            if p2 is None:
                newhead2, newend2 = f1(p1)
                break
            elif p2.next is None:
                newhead2, newend2 = f1(p1.next)
                break
        
        # let's compare
        v1 = dummyHead.next
        v2 = newhead2
        
        while v1 != p1:
            if v2 is None:
                return False
            
            if v1.val != v2.val:
                return False
            
            v1 = v1.next
            v2 = v2.next
        
        # here, we know that v1 is at p1
        if v2 is None:
            return False
        
        return v1.val == v2.val
       
```



### Design Linked List

Sol 1: (unknown)

这个答案是以前做的，反正也不难，细心即可

```
class MyLinkedList:
    class ListNode:
        def __init__(self, val):
            self.val = val
            self.next = None
        
        def __init__(self, val, next):
            self.val = val
            self.next = Next
        
        
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.dummyHead = ListNode(0)
        

    def get(self, index: int) -> int:
        """
        Get the value of the index-th node in the linked list. If the index is invalid, return -1.
        """
        
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode.next is not None:
            # here, we know that tmpNode.next is a valid node, just check its index
            if i == index:
                # this is the one we want to search
                return tmpNode.next.val
            else:
                i += 1
                tmpNode = tmpNode.next
        
        # if here, there is no such node
        return -1
            
        

    def addAtHead(self, val: int) -> None:
        """
        Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list.
        """
        tmpNode = ListNode(val, self.dummyHead.next)
        self.dummyHead.next = tmpNode
        

    def addAtTail(self, val: int) -> None:
        """
        Append a node of value val to the last element of the linked list.
        """
        
        tmpNode = self.dummyHead
        
        while tmpNode.next is not None:
            tmpNode = tmpNode.next
        
        tmpNode.next = ListNode(val)
        

    def addAtIndex(self, index: int, val: int) -> None:
        """
        Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted.
        """
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode is not None:
            if i == index:
                # this is the right place
                newNode = ListNode(val, tmpNode.next)
                tmpNode.next = newNode
                return
            else:
                i += 1
                tmpNode = tmpNode.next
        
        return
        
        

    def deleteAtIndex(self, index: int) -> None:
        """
        Delete the index-th node in the linked list, if the index is valid.
        """
        
        i = 0
        tmpNode = self.dummyHead
        
        while tmpNode is not None and tmpNode.next is not None:
            if i == index:
                tmpNode.next = tmpNode.next.next
                return
            else:
                i += 1
                tmpNode = tmpNode.next
        return
            
        


# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)
```

### Merge Two Sorted Lists

Sol 1: (2020-01-20)

很简单，为了方便，设置一个dummyhead即可，没啥难度

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        p1 = l1
        p2 = l2
        
        dummyHead = ListNode()
        p3 = dummyHead
        
        
        while p1 is not None and p2 is not None:
            # both nodes are valid, compare them
            if p1.val <= p2.val:
                p3.next = p1
                p3 = p1
                p1 = p1.next
            else:
                p3.next = p2
                p3 = p2
                p2 = p2.next
        
        if p1 is None:
            p3.next = p2
        else:
            p3.next = p1
        
        return dummyHead.next
```



### Add Two Numbers

Sol 1: (2020-01-20)

思路很简单。只是要注意最后剩余carry=1的情况。要当心。我第一次code的时候忘了设置这个，导致错误。



```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        p1 = l1
        p2 = l2
        
        dummyHead = ListNode()
        p3 = dummyHead
        
        carry = 0
        
        while p1 is not None and p2 is not None:
            tmpSum = p1.val + p2.val + carry
            
            if tmpSum < 10:
                carry = 0
            else:
                tmpSum -= 10
                carry = 1
            
            tmpNode = ListNode(tmpSum)
            p3.next = tmpNode
            p3 = tmpNode
            
            p1 = p1.next
            p2 = p2.next
        
        if p1 is not None:
            p4 = p1
        else:
            p4 = p2
            
        while p4 is not None:
            tmpSum = p4.val + carry

            if tmpSum < 10:
                carry = 0
            else:
                tmpSum = 0
                carry = 1
            
            tmpNode = ListNode(tmpSum)
            p3.next = tmpNode
            p3 = tmpNode
            
            p4 = p4.next
        
        if carry == 1:
            p3.next = ListNode(1)
        return dummyHead.next
```

### Flatten a Multilevel Doubly Linked List

Sol 1: (2020-01-20)

首先直观感觉用递归来做，给定一个head，返回一个以head为开头的flatten list，同时返回头尾即可。

但是居然submit居然没通过 看看怎么回事儿

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        def func_flatten(h):
            # input is a head node 
            # return the begin, end of a flatten list
            if h.next is None and h.child is None:
                # this is a single node, just return it
                return h, h
            elif h.next is not None and h.child is None:
                b, e = func_flatten(h.next)
                h.next = b
                b.prev = h
                return h, e
            elif h.next is None and h.child is not None:
                b, e = func_flatten(h.child)
                h.next = b
                b.prev = h
                h.child = None
                return h, e
            else:
                b, e = func_flatten(h.child)
                
                e.next = h.next
                h.next.prev = e
                
                h.next = b
                b.prev = h
                h.child = None
                
                return h, e
        
        h, e = func_flatten(head)
        return h
```

快速反思一下，因为这个是递归的，所以我要保证flatten以后，所有的child field全部为空。上面的可能没有注意这个 再看一下 呵呵

OK 找到问题了，还是递归的问题。当h同时有孩子和next的时候，必须同时对child 和next调用func，然后拼接三个list。我上面的代码只是拼接了两个 难怪错了 呵呵

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        def func_flatten(h):
            # input is a head node 
            # return the begin, end of a flatten list
            if h.next is None and h.child is None:
                # this is a single node, just return it
                return h, h
            elif h.next is not None and h.child is None:
                b, e = func_flatten(h.next)
                h.next = b
                b.prev = h
                return h, e
            elif h.next is None and h.child is not None:
                b, e = func_flatten(h.child)
                h.next = b
                b.prev = h
                h.child = None
                return h, e
            else:
                
                b, e = func_flatten(h.child)
                
                b2, e2 = func_flatten(h.next)
                
                h.next = b
                b.prev = h
                h.child = None
                
                e.next = b2
                b2.prev = e
                
                return h, e
        
        h, e = func_flatten(head)
        return h
```

居然还不对 看看为啥，

```
Input:
[1,2,3,4,5,6,null,null,null,7,8,9,10,null,null,11,12]
Output:
[1,2,3,7,8,11,12,4,5,6]
Expected:
[1,2,3,7,8,11,12,9,10,4,5,6]
```

好吧，仔细看了一下，上面饭了两个错误，一个是没有考虑head本身为空的情况，这个很好处理

另外一个是，当h同时有child and next的时候 最后返回的应该是h, e2而不是e 改了就好了 呵呵

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val, prev, next, child):
        self.val = val
        self.prev = prev
        self.next = next
        self.child = child
"""

class Solution:
    def flatten(self, head: 'Node') -> 'Node':
        def func_flatten(h):
            # input is a head node 
            # return the begin, end of a flatten list
            if h is None:
                return None, None
            
            if h.next is None and h.child is None:
                # this is a single node, just return it
                return h, h
            elif h.next is not None and h.child is None:
                b, e = func_flatten(h.next)
                h.next = b
                b.prev = h
                return h, e
            elif h.next is None and h.child is not None:
                b, e = func_flatten(h.child)
                h.next = b
                b.prev = h
                h.child = None
                return h, e
            else:
                b, e = func_flatten(h.child)
                b2, e2 = func_flatten(h.next)
                
                h.next = b
                b.prev = h
                h.child = None
                
                e.next = b2
                b2.prev = e
                
                return h, e2
        
        h, e = func_flatten(head)
        return h
```

### Insert into a Cyclic Sorted List

Sol 1: (2020-01-20)

直观来看很容易，感觉上使用双指针即可，没啥难度。

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    def insert(self, head: 'Node', insertVal: int) -> 'Node':
        
        if head is None:
            head = Node(insertVal)
            head.next = head
            return head
        elif head.next == head:
            # this is a single node loop
            tmpNode = Node(insertVal, head)
            head.next = tmpNode
            return head
        elif head.next.next == head:
            # this is a two node loop
            tmpNode = Node(insertVal, head.next)
            head.next = tmpNode
            return head
        
        # here, curr nodes >=3, we need to handle it
        p1 = head
        p2 = head.next
        
        tmpNode = Node(insertVal)
        while True:
            if p1.val <= p2.val:
                if p1.val <= insertVal and insertVal <= p2.val:
                    p1.next = tmpNode
                    tmpNode.next =p2
                    return head
                else:
                    p1 = p2
                    p2 = p2.next
            else:
                # here, we know that p1 is the largest val, p2 is the smallest val
                if insertVal >= p1.val or insertVal <= p2.val:
                    p1.next = tmpNode
                    tmpNode.next = p2
                    return head
                else:
                    p1 = p2
                    p2 = p2.next
```

上面这个超时了，错误如下

```
Last executed input:
[3,3,3]
0
```

感觉上，好像是死循环了，根据这个提示，增加了死循环检测，就可以了 呵呵

```
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    def insert(self, head: 'Node', insertVal: int) -> 'Node':
        
        if head is None:
            head = Node(insertVal)
            head.next = head
            return head
        elif head.next == head:
            # this is a single node loop
            tmpNode = Node(insertVal, head)
            head.next = tmpNode
            return head
        elif head.next.next == head:
            # this is a two node loop
            tmpNode = Node(insertVal, head.next)
            head.next = tmpNode
            return head
        
        # here, curr nodes >=3, we need to handle it
        p1 = head
        p2 = head.next
        
        tmpNode = Node(insertVal)
        while True:
            if p1.val <= p2.val:
                if p1.val <= insertVal and insertVal <= p2.val:
                    p1.next = tmpNode
                    tmpNode.next =p2
                    return head
            else:
                # here, we know that p1 is the largest val, p2 is the smallest val
                if insertVal >= p1.val or insertVal <= p2.val:
                    p1.next = tmpNode
                    tmpNode.next = p2
                    return head
            p1 = p2
            p2 = p2.next
            
            if p1 == head:
                # we have travel one full cycle
                p1.next = tmpNode
                tmpNode.next = p2
                return head
```



### Copy List with Random Pointer

Sol 1: (2020-01-20)

根据next来copy很简单。难度在于random怎么确定？

暂时的想法是，首先遍历依次，拿到每个node的遍历序号，同时简历ht: node <==>序号

然后第二次遍历，random node ==> 序号 ==> random node即可

```
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if head is None:
            return None
        
        ht_node_id = {} # for old list
        ht_id_node = {} # for new list
        
        dummyHead1 = Node(0)
        dummyHead2 = Node(0)
        
        p1 = dummyHead1
        p2 = dummyHead2
        i = 0
        
        while p1.next is not None:
            # p1.next is a valid node, copy it
            
            tmpNode = Node(p1.val)
            p2.next = tmpNode
            
            ht_node_id[p1.next] = i
            ht_id_node[i] = p2.next
            
            p1 = p1.next
            p2 = p2.next
            i += 1
        
        p1 = dummyHead1
        p2 = dummyHead2
        i = 0
        while p1.next is not None:
            if p1.next.random is None:
                p2.next.random = None
            else:
                curr_i = ht_node_id[p1.next.random]
                curr_node = ht_id_node[curr_i]
                p2.next.random = curr_node
            
            p1 = p1.next
            p2 = p2.next
            i += 1
        
        return dummyHead2.next
```

上面有问题

```
Your input
[[7,null],[13,0],[11,4],[10,2],[1,0]]
Your answer
[]
Expected answer
[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

仔细看了一下，发现是dummyHead1没有和原来的head连接上，重新来

```
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if head is None:
            return None
        
        ht_node_id = {} # for old list
        ht_id_node = {} # for new list
        
        dummyHead1 = Node(0, head)
        dummyHead2 = Node(0)
        
        p1 = dummyHead1
        p2 = dummyHead2
        i = 0
        
        while p1.next is not None:
            # p1.next is a valid node, copy it
            
            tmpNode = Node(p1.val) # error 其实应该是p1.next.val 改了就好了 呵呵
            p2.next = tmpNode
            
            ht_node_id[p1.next] = i
            ht_id_node[i] = p2.next
            
            p1 = p1.next
            p2 = p2.next
            i += 1
        
        p1 = dummyHead1
        p2 = dummyHead2
        i = 0
        while p1.next is not None:
            if p1.next.random is None:
                p2.next.random = None
            else:
                curr_i = ht_node_id[p1.next.random]
                curr_node = ht_id_node[curr_i]
                p2.next.random = curr_node
            
            p1 = p1.next
            p2 = p2.next
            i += 1
        
        return dummyHead2.next
```

还是不行

```
Your input
[[7,null],[13,0],[11,4],[10,2],[1,0]]
Your answer
[[0,null],[7,0],[13,4],[11,2],[10,0]]
Expected answer
[[7,null],[13,0],[11,4],[10,2],[1,0]]
```

### Rotate List

Sol 1: (2020-01-20)

首先，获取整个list的长度N，然后对K取模，再使用快慢指针做即可

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if head is None or head.next is None:
            return head
        
        # here, len(list) >= 2
        N = 0
        p = head
        while p is not None:
            N += 1
            p = p.next
        
        # N is the len list
        k = k % N
        
        if k == 0:
            return head
        
        fast = head
        for i in range(k):
            fast = fast.next
        
        slow = head
        
        while fast.next is not None:
            fast = fast.next
            slow = slow.next
        
        # here, fast is at the end node
        newhead = slow.next
        fast.next = head
        slow.next = None
        return newhead
```



### Find Pivot Index

Sol 1: (2020-01-20)

首先，排除暴力做法。

可以同时维护L R 每次迭代更新nums[i]即可，线性时间

```
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        N = len(nums)
        if N == 0:
            return -1
        elif N == 1:
            return 0
        
        # here, len(list) >= 2
        L = 0
        R = sum(nums)
        for i in range(N):
            R -= nums[i]
            
            if L == R:
                return i
            else:
                L += nums[i]
        return -1
```

### Largest Number At Least Twice of Others

Sol 1: (2020-01-20)

好像也不难，遍历一次即可，遍历的时候同时维护两个val即可

```
class Solution:
    def dominantIndex(self, nums: List[int]) -> int:
        N = len(nums) 
        if N == 1:
            return 0
        
        # here, len(nums) >= 2
        a , b = nums[0], nums[1]
        res = 1
        if a > b:
            a, b = b, a
            res = 0
        
        for i in range(2, N):
            curr_val = nums[i]
            if curr_val <= a:
                continue
            elif curr_val <= b:
                a = curr_val
            else: # curr_val > b
                a = b
                b = curr_val
                res = i
        
        if 2*a <= b:
            return res
        else:
            return -1
```

### Plus One

Sol 1: (2020-01-20)

直接操作digits最简单。反着来就可以了，没啥难度

```
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        digits[-1] += 1
        
        if digits[-1] != 10:
            return digits

        carry = 1
        digits[-1] = 0
        N = len(digits)
        
        i = -2
        while i >= -N:
            digits[i] += carry
            
            if digits[i] < 10:
                return digits
            else:
                digits[i] = 0
                carry = 1
            
            i -= 1
        
        if carry == 0:
            return digits
        else:
            return [1] + digits
```

