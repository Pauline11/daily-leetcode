# **leetcode 每日刷题**

## Day 1         --  Arrray (easy)

### 1. Two Sum



- 自己写的超越3.3%![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\SGPicFaceTpBq\7052\006A202E.png):

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

- 大佬写的百分百：

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

要求：原地修改 + 返回长度（没认真审题还被群里大佬推荐去看中文版。真的是暴

​		风哭泣）

没审题版本：![1543646807911](C:\Users\ADMINI~1\AppData\Local\Temp\1543646807911.png)

参考大佬版本1( 88 ms  + 33%）：

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

版本2:（72 ms + 	61%):

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
                                        

s = Solution()
print(s.removeDuplicates([1,1,2,3,4,4,4]))
```

