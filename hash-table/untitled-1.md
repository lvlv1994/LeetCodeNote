# 409. Longest Palindrome

 注意是+=2 而不是1 哦

```text
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        dic = {}
        result = 0
        for char in s:

            if char not in dic:
                dic[char] = 1
            else:
                result += 2
                del dic[char]
        return result if len(dic) == 0 else result + 1
```

