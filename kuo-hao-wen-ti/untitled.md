# 22. Generate Parentheses

注意之后的backpropagation

`class Solution(object):`

    `def generateParenthesis(self, n):`

        `"""`

        `:type n: int`

        `:rtype: List[str]`

        `"""`

        `self.result = []`

        `self.ans = []`

        `self.helper(n,n)`

        `return self.result`

    `def helper(self,left,right):`

        `if left > right:`

            `return`

        `print(self.ans,'before')`

        `if left == 0 and right == 0:`

            `self.result.append(''.join(self.ans))`

            `print(self.ans)`

            `self.ans.pop()`

            `return`

        `if left > 0 and left <= right:`

            `self.ans.append('(')`

            `self.helper(left-1,right)`

        `if right > 0 and left < right:`

            `self.ans.append(')')`

            `self.helper(left,right-1)`

        `if self.ans != []:`

            `self.ans.pop()`

            ``



