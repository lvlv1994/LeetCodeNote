# 518 Coin Change 2

`Remember to reverse coins and amount! To avoid duplicate!!`

`class Solution(object):`

    `def change(self, amount, coins):`

        `"""`

        `:type amount: int`

        `:type coins: List[int]`

        `:rtype: int`

        `"""`

        `import sys`

        `dp = [0 for i in range(amount+1)]`

        `dp[0] = 1`

        `for j in range(len(coins)):`    

            `for i in range(amount+1):`           

                `if i - coins[j] >= 0:`

                    `dp[i] += dp[i-coins[j]]`

        `return dp[-1]`

