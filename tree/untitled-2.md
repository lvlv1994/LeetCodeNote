# 257. Binary Tree Paths

没加一次,记得都要弹出，所以在root加的时候，记得弹出

`class Solution:`

    `def binaryTreePaths(self, root):`

        `"""`

        `:type root: TreeNode`

        `:rtype: List[str]`

        `"""`

        `if root is None:`

            `return []`

        `self.result = []`

        `self.ans = []`

        `self.helper(root)`

        `return self.result`

    `def helper(self,root):`

       ``

        `if root.left is None and root.right is None:`

            `self.ans.append(str(root.val))`

            `self.result.append(''.join(self.ans[:]))`

            `#self.ans.pop()`

            `return`

        `self.ans.append(str(root.val))`

        `self.ans.append('->')`



        `if root.left is not None:`

            `self.helper(root.left)`

            ``

        `if root.right is not None:`

            `self.helper(root.right)`

        `self.ans = self.ans[:-2]`

  ``    

  

 

