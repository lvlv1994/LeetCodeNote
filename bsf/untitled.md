# 499. The Maze III

Dijkstra 用一个list记录下来～然后sort, 因为要返回所有路径，所以更新的时候要记得&gt;=这种情况！!

`class Solution(object):`

    `def findShortestWay(self, maze, ball, hole):`

        `"""`

        `:type maze: List[List[int]]`

        `:type ball: List[int]`

        `:type hole: List[int]`

        `:rtype: str`

        `"""`

        `import sys`

        `self.dx = [1,0,0,-1]`

        `self.dy = [0,-1,1,0]`

        `self.dir = ['d','l','r','u']`

        `sets = set()`

        `distance = [[sys.maxsize for _ in range(len(maze[0]))] for _ in range(len(maze))]`

        `distance[ball[0]][ball[1]] = 0`

        `import Queue`

        `results = []`

        `q = Queue.PriorityQueue()`

        `q.put((0,ball[0],ball[1],''))`

        `while q.qsize()!=0:`

            `length,x,y,path = q.get()`

            `sets.add((x,y))`

            `#print(x,y,path,'a')`

            `if x == hole[0] and y == hole[1]:`

                    `results.append(path)`

            `for i in range(4):`

                ``

                `new_x,new_y,new_length = self.move(i,x,y,maze,sets,hole)`

                `#print(new_x,new_y,new_length,distance[new_x][new_y],'c')`

                `if distance[new_x][new_y] >= distance[x][y]+new_length and (new_x,new_y) not in sets:`

                    `#print(new_x,new_y,new_length,i,path,path + self.dir[i])`                  



                    `q.put((distance[x][y] + new_length, new_x, new_y, path + self.dir[i],))`



                    `distance[new_x][new_y] = distance[x][y]+new_length`

                        ``

        `results = sorted(results)`

    ``

        `return "impossible" if len(results) == 0 else results[0]`

                                  ``

                ``

    `def move(self,direction,x,y,maze,sets,hole):`

        `length = 0`

        ``

        `while self.isValid(maze,x+self.dx[direction],y+self.dy[direction],sets):`

            ``

            `if x == hole[0] and y ==hole[1]:`

                `#print(x,y,'hole')`

                `break`

                ``

            `x += self.dx[direction]`

            `y += self.dy[direction]`

            `#print(x,y)`

            `length += 1`

        `#print(direction,x,y,length)`   

        `return (x,y,length)`

            ``

    `def isValid(self,maze,x,y,sets):`

        `if x < len(maze) and y < len(maze[0]) and x >= 0 and y >= 0 and maze[x][y]!= 1:`

            `return True`

        `return False`





