# 213. House Robber II

同House Robber1 一样，这次不同的是他是一个环，那么我们只需要调用两次1的函数，一次输入截取掉头，第二次截取掉尾就可以了，值得注意的是，如果input的长度为1, 需要返回那个值

```text
class Solution:    def rob(self, nums):        """        :type nums: List[int]        :rtype: int        """        if nums ==[]:            return 0        if len(nums) == 1:            return nums[0]        return max(self.helper(nums[:-1]),self.helper(nums[1:]))    def helper(self,nums):        rob = nums[0]        not_rob = 0        for i in range(1,len(nums)):            tmp = not_rob            not_rob = max(rob,not_rob)            rob = nums[i] + tmp        return max(rob,not_rob)
```

