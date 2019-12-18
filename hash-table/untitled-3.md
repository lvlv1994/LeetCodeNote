# 451. Sort Characters By Frequency

注意bucketSort的基本思路，bucketSort用于找frequency

```text
class Solution(object):
    def frequencySort(self, s):
        """
        :type s: str
        :rtype: str
        """
        dic = {}
        bucket = [[] for _ in range(len(s)+1)]
        for char in s:
            if char not in dic:
                dic[char] = 1
            else:
                dic[char] += 1
        for d in dic:
            bucket[dic[d]].append(d)
        result = ''
        for i in range(len(bucket))[::-1]:
            for b in bucket[i]:
                result += b * i
        return result
            
```

