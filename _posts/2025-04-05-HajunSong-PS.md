---
layout: post
author: Hajun Song
tags: [ProblemSolving, BOJ]
---
[DFS와 BFS](https://www.acmicpc.net/problem/1260)
## Explanation

This problem outputs the results of searching a graph using DFS and BFS. 

Sample Input:
```
4 5 1
1 2
1 3
1 4
2 4
3 4
```
Sample Output:
```
1 2 4 3
1 2 3 4
```
## Implementation

**Time Complexity:** $\mathcal{O}(N + M)$

---
```python
from collections import deque
import sys 
input = sys.stdin.readline 
n,m,k = map(int,input().split())
arr = [[]for i in range(n+1)] 
d_v = [False for i in range(n+1)]
b_v = d_v[:]

for i in range(m):
    x,y = map(int,input().split())
    arr[x].append(y)
    arr[y].append(x)
for i in arr:i.sort()

def dfs(v): # DFS
    if d_v[v]:return
    print(v, end=' ') # Print
    d_v[v] = True
    for i in arr[v]:dfs(i)

dfs(k)
print()

def bfs(v): # BFS
    que = deque([v])
    while len(que) != 0:
        x = que.popleft()
        if not b_v[x]:
            b_v[x] = True
            print(x,end=' ') # Print
            for i in arr[x]:
                if not b_v[i]:que.append(i)
bfs(k)
```
