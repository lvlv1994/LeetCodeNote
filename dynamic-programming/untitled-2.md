---
description: >-
  https://leetcode.com/problems/house-robber-ii/discuss/59934/Simple-AC-solution-in-Java-in-O(n)-with-explanation
---

# 213. House Robber II

同House Robber1 一样，这次不同的是他是一个环，那么我们只需要调用两次1的函数，一次输入截取掉头，第二次截取掉尾就可以了，值得注意的是，如果input的长度为1, 需要返回那个值.

For nums\[0..n-1\], 0 and n-1 are neighboring to each other. Basically, there are only three possible cases: \(1\) rob 0, but leave n-1 untouched, \(2\) leave 0 untouched, rob n-1, \(3\) leave both 0 and n-1 untouched. Obviously, case \(3\) can be covered by case\(1\) or case \(2\) in the simple House Robber problem. Hence, the above solution covers all the possible cases.



```text
class Solution:
    def rob(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if nums ==[]:
            return 0
        if len(nums) == 1:
            return nums[0]
        return max(self.helper(nums[:-1]),self.helper(nums[1:]))
    def helper(self,nums):

        rob = nums[0]
        not_rob = 0
        for i in range(1,len(nums)):
            tmp = not_rob
            not_rob = max(rob,not_rob)
            rob = nums[i] + tmp
        return max(rob,not_rob)
```

