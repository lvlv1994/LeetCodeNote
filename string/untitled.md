# 7. Reverse Integer

```text
class Solution:
    def reverse(self, x: int) -> int:
        sign = 1
        if x < 0:
            sign = -1
        new_str = str(abs(x))[::-1]
        num = int(new_str) * sign
        if num > 2 ** 31 or num < -(2 ** 31) + 1:
            return 0
        return int(new_str) * sign
```

