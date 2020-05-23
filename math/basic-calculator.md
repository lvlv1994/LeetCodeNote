# Basic Calculator

一个tle的版本，每次找到最该算的那个符号，然后recursive的计算

```text
import sys
class Solution:
    
    def calculate(self, s: str) -> int:
        return self.helper(s)
        
    def findLastOp(self, exp):
        lastLoc = -1
        currPrivilege = 0
        hasAddSub = False
        ops = {"+", "-", "*", "/"}
        for i in range(len(exp)):
            e = exp[i]
            if e == '(':
                currPrivilege += 1 
            elif e == ')':
                currPrivilege -= 1
            if e in ops:
                #这里加=号是因为我们bydefault用的left associate，就是即使没有括号
                #我们也默认给左边同样privilege的条件加了括号
                if currPrivilege == 0:
                    if e in {"+", "-"}:
                        lastLoc = i
                        hasAddSub = True
                    elif hasAddSub == False:
                        lastLoc = i 
   
        return lastLoc
                    
    def helper(self, s):
        s = s.strip()
        #print(s, s.isdigit())
        if s.isdigit():
            return int(s)
        loc = self.findLastOp(s)
        
        #处理 （1+2）的情况，这样计算是避免（1+2）* （3+4）被误伤
        if loc == -1 and s[0] == '(':
            return self.helper(s[1:-1])
        #print(s, "the location is",  loc, shouldStripped,s[:loc],s[:loc].strip('('), s[loc+1:], s[loc+1:].strip(')'))
        left = self.helper(s[:loc])
        right = self.helper(s[loc+1:])
        #print('left+right', left, right)
        if s[loc] == '+':
            return left + right
        if s[loc] == '-':
            return left - right 
        if s[loc] == '*':
            return left * right
        if s[loc] == '/':
            return left / right
        
```

