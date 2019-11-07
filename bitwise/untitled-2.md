# 397. Integer Replacement

 [https://leetcode.com/problems/integer-replacement/discuss/87920/A-couple-of-Java-solutions-with-explanations?page=2](https://leetcode.com/problems/integer-replacement/discuss/87920/A-couple-of-Java-solutions-with-explanations?page=2)

解释的十分清楚

```text
class Solution:    def integerReplacement(self, n):        """        :type n: int        :rtype: int        """        c = 0        while n != 1:            if (n&1) == 0:                n = n >> 1            elif (n == 3) or bin(n+1).count('1') > bin(n-1).count('1'):                n -= 1            else:                n += 1            c += 1        return c
```

