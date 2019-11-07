---
description: >-
  https://leetcode.com/problems/beautiful-arrangement-ii/discuss/106965/Python-Straightforward-with-Explanation
---

# 667. Beautiful Arrangement II

操作神奇

```text
class Solution(object):    def constructArray(self, n, k):        """        :type n: int        :type k: int        :rtype: List[int]        """        ans = [i for i in range(1,n-k)]        print(ans)        for d in range(k+1):            if d % 2 == 0:                ans.append(n-k+d/2)            else:                ans.append(n-d/2)        print(ans)        return ans        
```

