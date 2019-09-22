# Ugly number

就是个数学性质，一直除质数就可以啦

```text
class Solution(object):
    def isUgly(self, num):
        """
        :type num: int
        :rtype: bool
        """
        for n in (2,3,5):
            while num % n == 0:
                num /= n
        return num == 1
```

