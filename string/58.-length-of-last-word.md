# 58. Length of Last Word

```text
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        if s.strip() == '' or s is None:
            return 0
        split = s.split()
        return len(split[-1])
```

