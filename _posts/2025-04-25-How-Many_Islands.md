---
layout: post
author: Hajun Song
tags: [ProblemSolving, BOJ]
---
[How Many Islands?](https://www.acmicpc.net/problem/4963)
## Explanation

You are given a marine area map that is a mesh of squares, each representing either a land or sea area. Figure B-1 is an example of a map.You can walk from a square land area to another if they are horizontally, vertically, or diagonally adjacent to each other on the map. Two areas are on the same island if and only if you can walk from one to the other possibly through other land areas. The marine area on the map is surrounded by the sea and therefore you cannot go outside of the area on foot.

Sample Input:
```
1 1
0
2 2
0 1
1 0
3 2
1 1 1
1 1 1
5 4
1 0 1 0 0
1 0 0 0 0
1 0 1 0 1
1 0 0 1 0
5 4
1 1 1 0 1
1 0 1 0 1
1 0 1 0 1
1 0 1 1 1
5 5
1 0 1 0 1
0 0 0 0 0
1 0 1 0 1
0 0 0 0 0
1 0 1 0 1
0 0
```
Sample Output:
```
0
1
1
3
1
9
```

### DFS: Depth First Search 
In DFS for a graph, we traverse all adjacent vertices one by one. When we traverse an adjacent vertex, we finish the traversal of all vertices reachable through that adjacent vertex.

## Implementation

**Time Complexity:** $\mathcal{O}(W * H)$

---
```python
import sys # import sys
sys.setrecursionlimit(100000) # make longer ricursive

def dfs(x,y): # dfs
    if visited[y][x]:return
    visited[y][x] = True
    if arr[y][x] == 0:return
    for i in range(x-1,x+2): # check Islands
        for j in range(y-1,y+2):
            if 0<=i<=w-1 and 0<=j<=h-1 and (i!=x or j!=y):
                dfs(i,j)


w,h = map(int,input().split()) # first input
while w!=0 and h!=0:
    arr = [[int(i) for i in input().split()]for i in range(h)]
    visited = [[False for i in range(w)] for _ in range(h)]
    cnt = 0
    for i in range(w):
        for j in range(h):
            if arr[j][i]==0 or visited[j][i]:
                visited[j][i]=True
            else:
                cnt+=1
                dfs(i,j)
    print(cnt)
    w,h = map(int,input().split()) # input
```
