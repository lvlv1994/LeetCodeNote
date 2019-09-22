# 47. Permutations II

sort一下数组，如果两个元素相等且前面这个元素没被访问过，说明当前情况下如果再访问前面那个元素，就一定有重复了

```text
class Solution:
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums = sorted(nums)
        self.visited = []
        self.ans = []
        self.result = []
        self.helper(nums)
        return self.result
    def helper(self,nums):
        if len(nums) == len(self.ans):
            self.result.append(self.ans[:])
            return
        for i in range(len(nums)):
            if i in self.visited or (i>0 and nums[i-1] == nums[i] and i-1 not in self.visited):
                continue
            self.visited.append(i)
            self.ans.append(nums[i])
            self.helper(nums)
            self.ans.pop()
            self.visited.pop()
        return
```

