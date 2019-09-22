# 考前偷看

1.  LRU: 建立双向链表和hash map,每次更新都把这个节点放到对尾， 查询的时候就是看看table里有没有

```text
class Node:
  def __init__(self, key = None, value = None):
      self.key = key
      self.val = value
      self.prev = None
      self.next = None
class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        # do intialization if necessary
        self.table = {}
        self.tail = Node(0,0)
        self.head = Node(0,0)
        self.capacity = capacity
        self.head.next = self.tail
        self.tail.prev = self.head
        
    """
    @param: key: An integer
    @return: An integer
    """
    def get(self, key):
        # write your code here
        if key in self.table:
            node = self.table[key]
            self.remove(node)
            self.move(node)
            return node.val
        return -1

    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self, key, value):
        # write your code here
        if key in self.table:
            node = self.table[key]
            node.val = value
            self.remove(node)
  
        else:
            
            if len(self.table) ==  self.capacity:
                node = self.head.next
                del self.table[node.key]
                self.head.next = self.head.next.next
                self.head.next.prev = self.head

            node = Node(key,value)
            self.table[key] = node

        self.move(node)
    def move(self,node):
        node.prev = self.tail.prev
        self.tail.prev = node
        node.prev.next = node
        node.next = self.tail
    def remove(self,node):
        node.prev.next = node.next
        node.next.prev = node.prev
        
            

```

2. 扫地机器人：建立world rigid 的moveleft，moveright,记录visited的点，且visited点不回溯!因为我们在做dfs

```text
def moveLeft(direction):
    turn_time = abs(direction-0)
    for i in range(turn_time):
        turnleft()
    if not move():
        for i in range(turn_time):
            #这里记得backtrack
            turnright()
        return False
    return True

```

3. Serialize and Deserialize Binary Tree

将树表达成1,2,3,\#,\#,4,5的形式,在建立树的时候，我们把他放到queue里, 然后弹出，如果是\#就为None,不然就递归

```text
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if root is None:
            return '#'
        left = self.serialize(root.left) 
        right = self.serialize(root.right)
        result = str(root.val) +','+left + ','+right
        print(result)
        return result
        
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data == '':
            return None
        fields = data.split(',')
        self.pos = 0
        import Queue
        q = Queue.Queue()
        for f in fields:
            q.put(f)
        root = self.deserialise(q)
        return root
    def deserialise(self,queue):
        node = queue.get()
        if node =='#':
            return None
        root = TreeNode(int(node))
        root.left = self.deserialise(queue)
        root.right = self.deserialise(queue)
        return root
        
```

4. **Merge k Sorted Lists**

就是建立一个priorityQueue，每次弹出最小节点以及放入他的下一个节点

```text
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        dummy = ListNode(0)
        curr = dummy
        import Queue
        q = Queue.PriorityQueue()
        for node in lists:
            if node:
                q.put((node.val,node))
        while q.qsize() > 0:
            curr.next = q.get()[1]
            curr = curr.next
            if curr.next:q.put((curr.next.val,curr.next))
        return dummy.next
```

5. party 中最大level和：

dfs,建立visited set, 每次传入上一次是不是被访问过了，如果没有，sun += val, 然后遍历他的孩子节点， 如果没有，只遍历孩子节点

6. word search

```text
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        self.ans = ''
        self.visited = []
        if len(board)== 1:
            return word in ''.join(board[0]) or word in ''.join(board[0])[::-1]
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == word[0]:
                    self.visited.append((i,j))
                    self.ans += word[0]
                    if self.helper(board,word,i,j):
                        
                        return True
                    self.visited.pop()
                    self.ans = ''
        return False
    def helper(self,board,word,row,col):
        if self.ans == word:
            return True
        elif len(self.ans) > len(word):
            return False
        dx = [1,0,-1,0]
        dy = [0,1,0,-1]
        for i in range(4):
            r,c = dx[i],dy[i]
            #print(self.ans)
            if self.isValid(row+r,col+c,board,word):      
               
                self.visited.append((row+r,col+c))
                self.ans += board[row+r][col+c]
         
                if self.helper(board,word,row+r,col+c):
                    return True
                self.visited.pop()
                self.ans = self.ans[:-1]
        return False
    def isValid(self,row_r,col_c,board,word):

        if 0 <= row_r < len(board) and 0 <= col_c < len(board[0]) and (row_r,col_c) not in self.visited and board[row_r][col_c] == word[len(self.ans)]:
            return True
        return False
        
```

7. kth largest:

```text
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
       
        start, end, rank = 0, len(nums)-1, len(nums)-(k-1)
        #random.shuffle(nums)
        while start <= end:
            ret = self._partition(nums, start, end)
            if ret == rank - 1:
                return nums[ret]
            elif ret < rank - 1:
                start = ret + 1
            else:
                end = ret - 1

    def _partition(self, nums, start, end):
        pivot = start

        while start < end:
            while nums[end] > nums[pivot] and end > start:
                end -= 1
            while nums[start] <= nums[pivot] and start < end:
                start += 1

            nums[start], nums[end] = nums[end], nums[start]

        nums[pivot], nums[start] = nums[start], nums[pivot]

        return start
        

```

8. Quick select:

```text
#!/usr/bin/env python2
# -*- coding: utf-8 -*-
"""
Created on Sun Apr 22 17:09:23 2018

@author: chunyilyu
"""

def quickSelect(k,inputs):
    start,end,rank = 0,len(inputs)-1,k   
    while start <= end:
        
        ret = partition(inputs,start,end)
        #print(inputs)
        if ret == rank-1:
            return inputs[ret]
        elif ret < rank - 1:
            start = ret + 1
        else:
            end = ret - 1
        

def partition(inputs,start,end):
    pivot = start
    while start < end:
        while inputs[end] > inputs[pivot] and start < end:
            end -= 1
        while inputs[start] <= inputs[pivot] and start < end:
            start += 1

        inputs[start],inputs[end] = inputs[end],inputs[start]
    inputs[pivot],inputs[start] = inputs[start],inputs[pivot]
    return start
inputs = [10, 9, 7, 6, 5, 4, 0]
print(quickSelect(3,inputs))
```

9. MergeSort

```text
#!/usr/bin/env python2
# -*- coding: utf-8 -*-
"""
Created on Sun Apr 22 17:53:04 2018

@author: chunyilyu
"""
def results(inputs):
    tmp = [0]*len(inputs)
    mergeSort(inputs,0,len(inputs)-1,tmp)
def mergeSort(inputs,left,right,tmp):
    if left >= right:
        return
    
    start = left
    end = right
    mid = (start+end)/2
    mergeSort(inputs,left,mid,tmp)
    mergeSort(inputs,mid+1,right,tmp)
    merge(inputs,left,mid,right,tmp)
def merge(inputs,left,mid,right,tmp):
    start = left
    end = mid+1
 
    index = start
    #print(start,end,mid)
    while start <= mid and end <= right:
        if inputs[start] < inputs[end]:
            tmp[index] = inputs[start]
            start += 1
        else:
            tmp[index] = inputs[end]
            end += 1
        index +=1
    while start <= mid:
        tmp[index] = inputs[start]
        start += 1
        index += 1
    while end <= right:
        tmp[index] = inputs[end]
        end += 1
        index += 1
    
    for index in range(left,right+1):
        #print(index)
        inputs[index] = tmp[index]

inputs = [2,3,4,10,7,9,12,13]
results(inputs)
```

10. Quick Sort;

11. Regular Expression Matching

```text
class Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        dp = [[False for i in range(len(p)+1)] for j in range(len(s)+1)]
        dp[0][0] = True
        for i in range(2,len(p)+1):
            if p[i-1] == '*':
                dp[0][i] = dp[0][i-2] 
        for i in range(1,len(s)+1):
            for j in range(1,len(p)+1):
                if s[i-1] == p[j-1] or p[j-1] == '.':
                    dp[i][j] = dp[i-1][j-1]
                elif p[j-1] == '*':
                    if s[i-1] == p[j-2] or p[j-2] == '.':
                        dp[i][j] = dp[i][j-2] | dp[i][j-1] | dp[i-1][j]
                    else:
                        dp[i][j] = dp[i][j-2]
        return dp[-1][-1]
```

