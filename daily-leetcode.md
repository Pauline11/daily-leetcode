# **LeetCode 每日刷题**

## Day 1         --  Array (easy)  

### 1. Two Sum



- 自己写的超越3.3%:

```python
"""
复杂度：O(n^2)
"""
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums) - 1):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
        return None

    
s = Solution()
print(s.twoSum([2, 7, 11, 15], 9))

```

- 大佬写的：

  ​

```python
"""
思路：将 (target - 遍历nums) 存入字典，作为键，并将值设为遍历的索引；
	继续遍历nums，直至找到与键相同的num,则返回此时字典中的索引以及
	nums的遍历索引 i ，即为所求。
	复杂度：O(n)
"""
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums) <= 1:
            return false
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]], i]
            else:
                buff_dict[target - nums[i]] = i

    
s = Solution()
print(s.twoSum([2, 7, 11, 15], 9))

```

### 26.Remove Duplicates from Sorted Array

要求：原地修改 + 返回***长度***（没认真审题还被群里大佬推荐去看中文版。真的是暴

​		风哭泣）

没审题版本：![1543646807911](C:\Users\ADMINI~1\AppData\Local\Temp\1543646807911.png)

参考大佬版本1：

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) <= 1:
            return len(nums)
        else :
            new_tag = 0
            for i in range(1, len(nums)):
                if nums[i] != nums[new_tag]:
                    new_tag += 1
                    nums[new_tag] = nums[i]
        return new_tag + 1
                                        

s = Solution()
print(s.removeDuplicates([1,1,2,3,4,4,4]))
```

版本2:

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        else :
            new_tag = 0
            for i in range(1, len(nums)):
                if nums[i] != nums[new_tag]:
                    new_tag += 1
                    nums[new_tag] = nums[i]
        return new_tag + 1
```

## Day  2

### 27.Remove Element

> **Description:**" Given an array *nums* and a value *val*, remove all instances of that 	value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory. "
>

```python
class Solution:
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        if not nums:
            return 0
        nums_len = 0
        for i in range(len(nums)):
            if nums[i] != val:
                nums[nums_len] = nums[i]
                nums_len += 1
        return nums_len
```

**Conclusion**:和26题很相似，删除指定元素，要求**原地修改**并**返回**修改后的列表***长度***。定义一个标签变量，记录长度。

### 35.Search Insert Position

> **Description**:Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.You may assume no duplicates in the array.
>

- 返回***位置索引***。自己写的，首先把目标值出现的三种特殊情况：小于最小值、等于最大值、大于最大值，单独拿出来讨论，然后遍历列表，相等就返回索引，不相等就判断target如果大于i的值并小于后一个值，返回索引+1,有点复杂。

```python
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums or target < nums[0]:
            return 0
        elif target == nums[-1]:
            return len(nums) - 1
        elif target > nums[-1]:
            return len(nums)
        for i in range(len(nums) - 1):
            if target == nums[i]:
                return i
            elif target > nums[i] and target < nums[i+1]:
                return i+1
            
                
```

- 大佬写的(Binary Search) 看完突然意识到，这是个搜索查找问题啊。二分查找啊！相等直接返回，不等就分，最后返回左边界。多么优秀的答案！

```python
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        l, r = 0, len(nums) -1 
        while l <= r:
            mid = (l + r) // 2
            if target == nums[mid]:
                return mid
            elif target < nums[mid]:
                r = mid - 1
            else:
                l = mid + 1
        return l
```

## Day  3

### 53.Maximum Sub-Array

- 返回最大的子数组***之和***。没想出来。思路其实很巧妙。

```python
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        for i in range(1, len(nums)):
            if nums[i - 1] > 0:
                nums[i] += nums[i-1]
        return max(nums)
```

let me see see,in contrast,从索引 1 开始遍历，只需判断前一个数如果为正数，就与其值相加。毕竟负数越加越小。最后比较数组中的所有值并返回最大。

### 66.Plus One

**Description:**"Given a **non-empty** array of digits representing a non-negative integer, plus one to the integer.        The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.       You may assume the integer does not contain any leading zero, except the number 0 itself."

- 加一操作啊。自己写的。先判断最简单的情况，最后一位小于9，直接加一。然后就是一通瞎操作，先遍历转成字符串 然后强转整加一后再放到列表中，很优秀的同时增加了空间复杂度和时间复杂度。

```python
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        if digits[-1] < 9:
            digits[-1] += 1
            return digits
        s = ''
        lst = []
        for i in digits:
            s += str(i)
        int_s = int(s) + 1

        for j in str(int_s):
            lst.append(int(j))
        return lst
```

- 大佬的

```python
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        nums = 0
        for i in range(len(digits)):
            nums += digits[i] * pow(10, (len(digits) - 1 - i))
        return [int(i) for i in str(nums + 1)]



```

用到了pow(底数，指数)函数，直接遍历将各位乘权值加起来然后进行加一操作，然后转换成字符串。利用字符串的可遍历（迭代性），将每一位取出来放入列表并返回。

- [x] kp:**字符串是字符的有序集合，可以通过其位置来获得具体的元素。**

## Day  4  (12/06/2018)

### 118.Pascal's Triangle（I）

> **Description**:杨辉三角，Input: 5  Output:[     [1],    [1,1],   [1,2,1],  [1,3,3,1], [1,4,6,4,1]]
>

- 看完答案，发现自己思路是对的，但有些乱而且没去实现。还是写的少。

```python
class Solution:
    def generate(self, numRows):
        triangle = []
        for i in range(numRows):
            # initial
            row = [1] * (i + 1)
            triangle.append(row)
            # 每行只有首尾不需要修改的
            for j in range(1, len(row) - 1):
                row[j] = triangle[i-1][j-1] + triangle[i-1][j]
        return triangle
```

- 大佬的答案，用了map，但是我没跑出来。回头再看。

```python
def generate(self, numRows):
        res = [[1]]
        for i in range(1, numRows):
            res += [map(lambda x, y: x+y, res[-1] + [0], [0] + res[-1])]
        return res[:numRows]
    
"""explanation: Any row can be constructed using the offset sum of the previous row. Example:
    1 3 3 1 0 
 +  0 1 3 3 1
 =  1 4 6 4 1
 """
```

### 119.Pascal's Triangle(II)

> **Description**:Given a non-negative index *k* where *k* ≤ 33, return the *k*th index row  of the Pascal's triangle.Note that the row index starts from 0.
>

- 还是杨辉三角，不过给出数字i要求返回第(i+1)行的值

```python
class Solution:
    def getRow(self, rowIndex):
        tri = []
        for i in range(rowIndex + 1):
            row = [1] * (i + 1)
            tri.append(row)
            for j in range(1, len(row) - 1):
                row[j] = tri[i-1][j-1] + tri[i-1][j]
        return tri[-1]
        
```

