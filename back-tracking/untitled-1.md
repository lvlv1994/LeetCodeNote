# 47. Permutations II

sort一下数组，如果两个元素相等且前面这个元素没被访问过，说明当前情况下一定会出现之前已经出现的组合，应该跳过

```text
class Solution:
    
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        self.visited = []
        self.result = []
        for _ in range(len(nums)):
            self.visited.append(False)
        nums.sort()
        self.helper(nums, [])
        return self.result
    
    def helper(self, nums, ans):
        if len(nums) == len(ans):
            self.result.append(ans[:])
            return
        for i in range(len(nums)):
            if i != 0  and not self.visited[i-1] and nums[i] == nums[i - 1]:
                continue
            if self.visited[i]:
                continue
            self.visited[i] = True
            ans.append(nums[i])
            self.helper(nums, ans)
            self.visited[i] = False
            ans.pop()
        
```

