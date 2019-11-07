# 173. Binary Search Tree Iterator

建立一个stack，存储一路所有左节点，这样第一个pop出来的就是最左节了，如果他有右节点，做相同的事。值得注意solution里的这个回复：the Space complexity section in the first solution mentions `O(N)` rather than `O(h)`. It just says that `O(h)` is the space occupied by the recursion stack but in addition to that we also use the `nodes_sorted` array which occupies `O(N)` space which is the deal breaker.

```text
​class BSTIterator:    def __init__(self, root: TreeNode):        self.stack = []        self.left_most(root)            def left_most(self, root):        while root:            self.stack.append(root)            root = root.left    def next(self) -> int:        """        @return the next smallest number        """        top = self.stack.pop()                if top.right:            self.left_most(top.right)                return top.val    def hasNext(self) -> bool:        """        @return whether we have a next smallest number        """        return len(self.stack) > 0
```

