# House Robber III

分治，不偷为左右返回的最大值，偷为左右不偷相加

```text
class Solution:
    def rob(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        rob,not_rob = self.helper(root)
        return max(rob,not_rob)
    def helper(self,root):
        if root is None:
            return 0,0
        l_rob,l_not_rob = self.helper(root.left)
        r_rob,r_not_rob = self.helper(root.right)
        not_rob = max(l_rob,l_not_rob)+max(r_rob,r_not_rob)
        rob = l_not_rob+root.val+r_not_rob
        return rob,not_rob
```

