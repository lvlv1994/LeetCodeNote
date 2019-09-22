# 778. Swim in Rising Water

First use BFS to find weather is connect is a specific time slot, and if the endpoint is connected, return True, else return False.

Use Binary Search to find the connected time period since it's a permutation.

在某个时间下，终点是否包含在这个时间里（用bfs）:

`class Solution(object):`

    `def swimInWater(self, grid):`

        `"""`

        `:type grid: List[List[int]]`

        `:rtype: int`

        `"""`

        `start,end = 0,len(grid)*len(grid[0])-1`

        `while start <= end:`

            `mid = (start + end) / 2`

         ``

            `if not self.bfs(grid,mid):`

                `start = mid + 1`

            `else:`

                `end = mid - 1`           

        `return start`

              ``

    ``

    `def bfs(self,grid,time):`

        `import Queue`

        `visited = []`

        `q = Queue.Queue()`

        `dx = [1,0,-1,0]`

        `dy = [0,1,0,-1]`

        `if time >= grid[0][0]:`

            `q.put((0,0))`

        `else:`

            `return False`

        `while q.qsize()!= 0:`

            ``

            `node = q.get()`

            `for i in range(4):`

                `tmp = (node[0]+dx[i],node[1]+dy[i])`

                `if tmp not in visited and self.isValid(tmp,time,grid):`

                    `q.put(tmp)`

                    `visited.append(tmp)`

                    `if tmp == (len(grid)-1,len(grid[0])-1):`

                        `return True`

           ``

        `return False`

    `def isValid(self,tmp,time,grid):`

        `if tmp[0] < 0 or tmp[1] < 0 or tmp[0] >= len(grid) or tmp[1] >= len(grid[0]):`

            `return False`

        `elif grid[tmp[0]][tmp[1]] > time:`

            `return False`

        `return True`

  

