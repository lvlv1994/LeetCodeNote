# 297. Serialize and Deserialize Binary Tree

这道题本着如何建立树 如何deserlize树的原则

1. 层级便利
   1.   ```text
      class Codec:

          def serialize(self, root):
              """Encodes a tree to a single string.
        
              :type root: TreeNode
              :rtype: str
              """
              import queue
              q = queue.Queue()
              if not root:
                  return []
              result = []
              q.put(root)
        
              while q.qsize() != 0:
                  node = q.get()
                  if node:
                      result.append(node.val)
                      q.put(node.left)
                      q.put(node.right)
                  else:
                      result.append('null')
              return result
        
        

          def deserialize(self, data):
              """Decodes your encoded data to tree.
        
              :type data: str
              :rtype: TreeNode
              """
              if not data:
                  return None
              import queue
              q = queue.Queue()
              root = TreeNode(data[0])
              idx = 1
              q.put(root)
              while q and idx < len(data):
                  node = q.get()
                  if data[idx] != 'null':
                      left = TreeNode(data[idx])
                      node.left = left
                      q.put(left)
                  idx += 1
                  if data[idx] != 'null':
                      right = TreeNode(data[idx])
                      node.right = right
                      q.put(right)
                  idx += 1
            
              return root
      ```
2. preorder+dfs

```text
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        import queue
        q = queue.Queue()
        if not root:
            return []
        result = []
        q.put(root)
        
        while q.qsize() != 0:
            node = q.get()
            if node:
                result.append(node.val)
                q.put(node.left)
                q.put(node.right)
            else:
                result.append('null')
        return result
        
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if not data:
            return None
        import queue
        q = queue.Queue()
        root = TreeNode(data[0])
        idx = 1
        q.put(root)
        while q and idx < len(data):
            node = q.get()
            if data[idx] != 'null':
                left = TreeNode(data[idx])
                node.left = left
                q.put(left)
            idx += 1
            if data[idx] != 'null':
                right = TreeNode(data[idx])
                node.right = right
                q.put(right)
            idx += 1
            
        return root
```

```text
class Codec:

    def serialize(self, root):
        # write your code here
        if not root:
            return ['#']
        ans = []
        ans.append(str(root.val))
        ans += self.serialize(root.left)
        ans += self.serialize(root.right)
        return ans
            
    def deserialize(self, data):
        # write your code here
        ch = data.pop(0)
        if ch == '#':
            return None
        else:
            root = TreeNode(int(ch))
        root.left = self.deserialize(data)
        root.right = self.deserialize(data)
        return root

```



