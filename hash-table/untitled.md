# 387. First Unique Character in a String

建立map记录frequency， 然后从头再遍历一次字符串

```text
class Solution:    def firstUniqChar(self, s):        """        :type s: str        :rtype: int        """        dic = {}        for i in range(len(s)):            if s[i] not in dic:                dic[s[i]] = 1            else:                dic[s[i]] += 1        for i in range(len(s)):            #print(s[i],dic[s[i]])            if dic[s[i]] == 1:                return i        return -1
```

