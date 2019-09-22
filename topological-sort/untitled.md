# 444. Sequence Reconstruction

当qsize 不为1的时候返回false，当遍历长度不为所有点的时候返回false.值得注意的是我们建立图的时候务必建立所以边和点，不然会出错

```text
class Solution(object):
    def sequenceReconstruction(self, org, seqs):
        """
        :type org: List[int]
        :type seqs: List[List[int]]
        :rtype: bool
        """
        self.degree = {}
        self.adj = {}
        self.buildGraph(seqs)
        import Queue
        q = Queue.Queue()
        self.visited = set()
        for d in self.degree:
            if self.degree[d] == 0:
                q.put(d)
        i = 0
        #print(self.degree)
        while q.qsize()!=0:
        
            if q.qsize() != 1:
                return False
            node = q.get() 
            if node in self.visited:
                return False
            self.visited.add(node)
            if i == len(org) or node != org[i]:
                return False
            i += 1
            
            for edge in self.adj[node]:
                self.degree[edge] -= 1
                if self.degree[edge] == 0:
                    q.put(edge)
        return i == len(org) and i == len(self.degree)
                
    def buildGraph(self,seqs):
        for seq in seqs:
            if len(seq) == 1:
                if seq[0] not in self.degree:
                    self.degree[seq[0]] = 0
                    self.adj[seq[0]] = []
            else:
                for i in range(len(seq)-1):
                    e1,e2 = seq[i],seq[i+1]
                    if e1 not in self.adj:
                        self.adj[e1] = [e2]
                      
                    else:
                        #print(e1,seq,self.adj[e1])
                        self.adj[e1].append(e2)
                    if e2 not in self.degree:
                        self.degree[e2] = 1
                    else:
                        self.degree[e2] += 1
                    if e2 not in self.adj:
                        self.adj[e2] = []
                    if e1 not in self.degree:
                        self.degree[e1] = 0
            
                        
                
                
                
        
        
```

