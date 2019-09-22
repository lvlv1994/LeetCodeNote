# 401. Binary Watch

bin 就是把他转换成二进制

```text
class Solution(object):
    def readBinaryWatch(self, num):
        """
        :type num: int
        :rtype: List[str]
        """
        return ['%d:%02d' %(h,m) for h in range(12) for m in range(60) if (bin(h) + bin(m)).count('1') == num]
        
```

