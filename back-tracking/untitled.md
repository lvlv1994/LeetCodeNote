# 357. Count Numbers with Unique Digits

For every i, track down and return 1, then in this digit, try to count how many numbers are there totally, we set total as one because prefix is a valid number alreay, such as n = 3, 1or12 is valid too!! Or we can use dp too solve it!

`class Solution(object):`

    `def countNumbersWithUniqueDigits(self, n):`

        `"""`

        `:type n: int`

        `:rtype: int`

        `"""`

        `self.visited = []`

        `return self.helper(0,n)`

        ``

    `def helper(self,d,n):`

        `if d == n:`

            `return 1`

        `total = 1`

        `start = 0`

        `if d == 0:`

            `start =  1`

        `for i in range(start,10):`

            `if i not in self.visited:`

                `self.visited.append(i)`

                `total += self.helper(d+1,n)`

                `self.visited.pop()`

        `return total`

