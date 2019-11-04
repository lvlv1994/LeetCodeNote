# 417. Pacific Atlantic Water Flow

从边边到中间，建立两个matrix分别存储可不可以，然后and 一下

`class Solution(object):`

    `def pacificAtlantic(self, matrix):`

        `"""`

        `:type matrix: List[List[int]]`

        `:rtype: List[List[int]]`

        `"""`

        `if matrix == []:`

            `return []`

        `canPacific = [[False]*len(matrix[0]) for i in range(len(matrix))]`

        `canAtlantic = [[False]*len(matrix[0]) for i in range(len(matrix))]`

    ``

        `for i in range(len(matrix)):`

            `canPacific[i][0] = True`

            `canAtlantic[i][-1] = True`

        `for j in range(len(matrix[0])):`

            `canPacific[0][j] = True`

            `canAtlantic[-1][j] = True` 

        `#print(canPacific)`

        `for i in range(len(matrix)):`

            `self.dfs(canPacific,i,0,matrix)`

            `self.dfs(canAtlantic,i,len(matrix[0])-1,matrix)`

        `for j in range(len(matrix[0])):`

            `self.dfs(canPacific,0,j,matrix)`

            `self.dfs(canAtlantic,len(matrix)-1,j,matrix)` 

        ``

       ``



        `return [[i,j] for i in range(len(matrix)) for j in range(len(matrix[0])) if canPacific[i][j] and canAtlantic[i][j]]`

    ``

    `def dfs(self,matrix,row,col,ori):`

        `dx = [1,0,-1,0]`

        `dy = [0,1,0,-1]`

        `for i in range(4):`

            `new_x,new_y = row+dx[i],col+dy[i]`

            `if 0<=new_x<len(matrix) and 0 <=new_y<len(matrix[0]) and matrix[new_x][new_y] != True and ori[new_x][new_y]>=ori[row][col]:`

             ``

                `matrix[new_x][new_y] = True`

                `self.dfs(matrix,new_x,new_y,ori)`

            ``

            

        

        

