---
layout: post
author: SeungJoon Park
tags: [ProblemSolving , BOJ]
---

[BOJ 7562](https://www.acmicpc.net/problem/7562)

## Explanation

The main issue in this problem is to figure out the least number that the Knight requires to move to the desired place.

To do this, we can use BFS to find the shortest path that the Knight can move.
From the initial position, try to assess every position that the Knight can move. While doing this, exclude unable position (out of the board or already visited position). If the Knight arrived to the desired position, it will be the shortest path.

For example, let's look at the sample input:
```
1
8
0 0
7 0
```

From (0,0), find every position that the Knight can move. As it move, it will move closer to the desired position. 

With this knowledge, we can now iterate this process, trying all position and taking the minimum number for its movement.

## Implementation

**Time Complexity:** $\mathcal{O}(N^2)$


```py
from collections import deque

def bfs():
    queue.append(now)
    visited[now[0]][now[1]]

    while queue:
        x,y = queue.popleft()
        if x == dest[0] and y == dest[1]: return 0
        for i in range(8):
            nx = x+dx[i]
            ny = y+dy[i]

            if nx<0 or ny >= n or nx>=n or ny<0: continue
            if nx == dest[0] and ny == dest[1]: 
                visited[nx][ny] = True
                return matrix[x][y]+1
            if visited[nx][ny] == False:
                queue.append([nx,ny])
                visited[nx][ny] = True
                matrix[nx][ny] = matrix[x][y] + 1

for _ in range(int(input())):
    n = int(input())
    now = list(map(int,input().split()))
    dest = list(map(int,input().split()))

    matrix = [[0]*n for _ in range(n)]
    visited = [[False]*n for _ in range(n)]

    queue =deque()
    dx = [-2,-1,1,2,2,1,-1,-2]
    dy = [1,2,2,1,-1,-2,-2,-1]

    print(bfs())
```
