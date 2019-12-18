# 789. Escape The Ghosts

如果有一个ghost能提前到达target的话必输

```text
class Solution(object):
    def escapeGhosts(self, ghosts, target):
        """
        :type ghosts: List[List[int]]
        :type target: List[int]
        :rtype: bool
        """
        maximum = abs(target[0]) + abs(target[1])
        for ghost in ghosts:
            tmp = abs(ghost[0]-target[0]) + abs(ghost[1]-target[1])
            if tmp < maximum:
                return False
        return True
```



