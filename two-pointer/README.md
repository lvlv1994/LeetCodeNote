---
description: >-
  https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems
---

# Two pointer

有套路的

```text
class Solution(object):    def minWindow(self, s, t):        """        :type s: str        :type t: str        :rtype: str        """                dic = {}        for char in t:            if char in dic:                dic[char] += 1            else:                dic[char] = 1        counter = len(set(t))        start,end = 0,0        head = 0        import sys        d = sys.maxsize        while end < len(s):            if s[end] in dic:                dic[s[end]] -= 1            if s[end] in dic and dic[s[end]] == 0:                counter -= 1            while start <= end and counter == 0:                if end - start < d:                                        d = min(d,end-start)                    head = start                #print(start,end,dic,head,d,counter)                if start <= end and s[start] in dic and dic[s[start]] == 0:                                      counter += 1                if  s[start] in dic:                    dic[s[start]] += 1                start += 1            #print(start,end,dic,d,head,counter,'out')            end += 1        return '' if d == sys.maxsize else s[head:head+d+1]                
```

