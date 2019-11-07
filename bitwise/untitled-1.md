# 421. Maximum XOR of Two Numbers in an Array

curBit = \(num &gt;&gt; i\) & 1  这个是用来check在当前位是0还是1，然后build一个trie，check = curBit^1 这个是看opposite的方向有没有数字，如果有得话，就把这个位置对应的数加起来。就很厉害，时间复杂度32n

```text
class Solution:    def findMaximumXOR(self, nums):        """        :type nums: List[int]        :rtype: int        """        import sys        self.root = {}        maximum = -sys.maxsize        self.build(nums)        for num in nums:            node = self.root            curSum = 0            for i in range(32)[::-1]:                curBit = (num >> i) & 1                check = curBit^1                #print(node)                if check in node:                    curSum += (1 << i)                    node = node[check]                else:                    node = node[curBit]            maximum = max(curSum,maximum)        return maximum    def build(self,nums):        for num in nums:            node = self.root            for i in range(32)[::-1]:                curBit = (num >> i) & 1                if curBit not in node:                    node[curBit] = {}                node = node[curBit]
```

