# 173. Binary Search Tree Iterator

建立一个list，存储最左节点，每返回一次，就加一个右节点以及所有左节点

`class BSTIterator(object):`

    ``

    `def __init__(self, root):`

        `"""`

        `:type root: TreeNode`

        `"""`

        `self.root = root`

        `self.stack = []`

        `while root is not None:`

            `self.stack.append(root)`

            `root = root.left`

            ``

            ``

            ``

        ``

    `def hasNext(self):`

        `"""`

        `:rtype: bool`

        `"""`

        `return len(self.stack) != 0`

        ``



    `def next(self):`

        `"""`

        `:rtype: int`

        `"""`

        `node = self.stack.pop()`

        `tmp = node.right`

        `while tmp is not None:`

            `self.stack.append(tmp)`

            `tmp = tmp.left`

        `return node.val`

