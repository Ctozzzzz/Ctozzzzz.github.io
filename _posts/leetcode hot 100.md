# 代码

## 1. 两数之和
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 如果不在遍历里套遍历是否可以实现
        # 哈希映射 key:nums里的数值 values:数值对应的索引
        hashmap = {}
        for idx,num in enumerate(nums):
            goal = target - num
            if goal in hashmap:
                return [hashmap[goal], idx]
            hashmap[num] = idx
```
## 2. 两数相加
```python
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        # 单向链表只能从头到尾遍历 先加起来，进位留到后面
        # dummy保存头节点
        dummy = ListNode()
        carry, curr = 0, dummy
        while l1 or l2 or carry:
            s = (l1.val if l1 else 0) + (l2.val if l2 else 0) + carry
            carry, val = divmod(s, 10)
            # 余位作为新的链表拼接上去
            curr.next = ListNode(val)
            curr = curr.next
            # 继续遍历
            l1 = l1.next if l1 else None
            l2 = l2.next if l2 else None
        return dummy.next
```

## 3. 无重复字符的最长子串

滑动窗法，用set保存不重复的子串；一旦遇到重复字符，从左侧开始删除，直到除掉重复字符
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s: return 0
        left = 0
        lookup = set()
        max_len, cur_len = 0, 0

        for i in range(len(s)):
            cur_len += 1
            while s[i] in lookup:
                # 重复的情况 从左侧开始删除 直到跳过重复段
                lookup.remove(s[left])
                left += 1
                cur_len -= 1
            if cur_len > max_len: max_len = cur_len
            lookup.add(s[i])
        return max_len
```

## 4.寻找两个正序数组的中位数
```python

```

## 5. 最长回文子串
```python
class Solution:
    def expandAroundCenter(self, s, left, right):
        while left >=0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return left + 1, right - 1
    
    def longestPalindrome(self, s: str) -> str:
        # 中心拓展
        start, end = 0, 0
        for i in range(len(s)):
            # 回文串的两种情况: xxaxaxx xxaaxx
            left1, right1 = self.expandAroundCenter(s, i, i)
            left2, right2 = self.expandAroundCenter(s, i, i+1)
            if right1 - left1 > end - start:
                start = left1
                end = right1
            if right2 - left2 > end - start:
                start = left2
                end = right2
        return s[start:end+1]
```

## 10. 正则表达式匹配
```python

```

## 11. 盛最多水的容器
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        res = 0
        i ,j = 0, len(height) -1 
        while i < j:
            if height[i] < height[j]:
                # 向内移动短板，短板可能增大，面积可能增大；而向内移动长板，由于宽度变小，则面积一定变小
                res = max(res, height[i] * (j - i))
                i += 1
            else:
                res = max(res, height[j] * (j - i))
                j -= 1
        return res
```

## 15. 三数之和
```python

```