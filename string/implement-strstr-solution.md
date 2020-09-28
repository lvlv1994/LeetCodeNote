# Implement strStr\(\)Solution

```text
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        h, n = 0, 0
        if needle == "":
            return 0
        while h < len(haystack) - len(needle) + 1:
            idx = h
            while idx < len(haystack) and n < len(needle) and haystack[idx] == needle[n]:
                idx += 1
                n += 1
            if n == len(needle):
                return h
            n = 0
            h += 1
        return -1
            
```

