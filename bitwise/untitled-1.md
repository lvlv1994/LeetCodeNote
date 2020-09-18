# 421. Maximum XOR of Two Numbers in an Array

curBit = \(num &gt;&gt; i\) & 1  这个是用来check在当前位是0还是1，然后build一个trie，check = curBit^1 这个是看opposite的方向有没有数字，如果有得话，就把这个位置对应的数加起来。就很厉害，时间复杂度32n

```text
class Solution:
    def findMaximumXOR(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        import sys
        self.root = {}
        maximum = -sys.maxsize
        self.build(nums)
        for num in nums:
            node = self.root
            curSum = 0
            for i in range(32)[::-1]:
                curBit = (num >> i) & 1
                check = curBit^1
                #print(node)
                if check in node:
                    curSum += (1 << i)
                    node = node[check]
                else:
                    node = node[curBit]
            maximum = max(curSum,maximum)
        return maximum
    def build(self,nums):
        for num in nums:
            node = self.root
            for i in range(32)[::-1]:
                curBit = (num >> i) & 1
                if curBit not in node:
                    node[curBit] = {}
                node = node[curBit]
```

还有一个bitwise的方法

```text
class Solution:
    def findMaximumXOR(self, nums: List[int]) -> int:
        #bitwise解法， 从1000000开始， The maxResult is a record of the largest XOR we got so far.
        maxResult = 0
        mask = 0
        #从100000开始，然后是110000
        #The mask will grow like  100..000 , 110..000, 111..000,  then 1111...111
        #for each iteration, we only care about the left parts
        for i in range(32)[::-1]:
            mask = mask | 1 << i
            sets = {}
            #比如96是110000，对100000这个mask取就是100000
            for num in nums:
                left = num & mask
                sets[left] = 1
            #如果之前的maxResult是1010000，现在1 << i 是 1000，我们尝试在这个bit位置有没有
            #1011000的可能
            greedyTry = maxResult | (1 << i)
            
            for item in sets:
                #This is the most tricky part, coming from a fact that if a ^ b = c, then a ^ c = b;
                #所以我们挨个尝试，如果刚好有两个num的bit xor在这个位置是1，我们就更新maxResult，为1011000
                #如果没有，maxResult不更新，还是1010000
                anotherNum = greedyTry ^ item
                if anotherNum in sets:
                    maxResult = greedyTry
                    break
        return maxResult
```

