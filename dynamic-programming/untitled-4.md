# 651. 4 Keys Keyboard

比如我们可以操作7步，那么加入我们用了3（i）步做了AAA，然后城下7步，这7步应该是Ctrl A, Ctrl C, Ctrl V， Ctrl V， 所以有 n - i -1 个copy

```text
class Solution(object):
    def maxA(self, N):
        """
        :type N: int
        :rtype: int
        """
        dp = [i for i in range(N+1)]
        for i in range(1,N+1):
            for j in range(1,i-2):
                dp[i] = max(dp[i],dp[j]*(i-j-1))
        return dp[-1]
```

