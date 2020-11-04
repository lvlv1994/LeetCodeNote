# 332. Reconstruct Itinerary

注意每次加入result里都要返回在这个词典里删除词，然后在加回去

注意每次加入词典都要sort一下！

注意用index而不是child

注意一旦找到答案就返回，不然不是最优解！

```text
class Solution(object):
    def findItinerary(self, tickets):
        """
        :type tickets: List[List[str]]
        :rtype: List[str]
        """
        self.numTicket = len(tickets)
        tickets = sorted(tickets, key = lambda x: (x[0],x[1]))
        from collections import defaultdict
        graph = collections.defaultdict(list)
        for ticket in tickets:
            graph[ticket[0]].append(ticket[1])
        self.result = ["JFK"]
        self.final = []
        self.helper(graph,"JFK")
        return self.final
    def helper(self,graph,node):
        #print(graph,node,graph[node],self.result)
        if len(self.result) == self.numTicket + 1:
            self.final = self.result[:]
            return
        
        for i in range(len(graph[node])):
            child = graph[node][i]
            graph[node].remove(child)
            #print(graph)
            self.result.append(child)         
            self.helper(graph,child)     
            if len(self.result) == self.numTicket + 1:
                return
            graph[node].append(child)
            graph[node] = sorted(graph[node],key = lambda x:(x[0],x[1]))
            self.result.pop()
            #print(graph,node,child,'v')

```

