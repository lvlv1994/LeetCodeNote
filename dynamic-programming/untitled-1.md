# 44. Wildcard Matching

Thing like question 10

`class Solution(object):`

    `def isMatch(self, s, p):`

        `"""`

        `:type s: str`

        `:type p: str`

        `:rtype: bool`

        `"""`

        `dp = [[False for i in range(len(p)+1)] for j in range(len(s)+1)]`

        `dp[0][0] = True`

        `for i in range(1,len(p)+1):`

            `dp[0][i] = dp[0][i-1] and p[i-1]=='*'`

        `for i in range(1,len(s)+1):`

            `for j in range(1,len(p)+1):`

                `if p[j-1] == s[i-1] or p[j-1] == '?':`

                    `dp[i][j] = dp[i-1][j-1]`

                `elif p[j-1] == '*':`

                    `dp[i][j] = dp[i][j-1] | dp[i-1][j]`

        `return dp[-1][-1]`

