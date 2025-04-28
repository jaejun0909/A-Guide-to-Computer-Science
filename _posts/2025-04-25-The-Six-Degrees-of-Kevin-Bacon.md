---
layout: post
author: Hajun Song
tags: [ProblemSolving, BOJ]
---
[The Six Degrees of Kevin Bacon](https://www.acmicpc.net/problem/1389)
## Explanation

"Six Degrees of Kevin Bacon" is a popular game and cultural phenomenon based on the concept of the "small world" theory, which suggests that any two people on the planet can be connected through six degrees of separation. 

We're going to find the person with the smallest number of Kevin Bacon among Baekjoon Online Judge's users. The Kevin Bacon number is the sum of the steps that come out when you play the Kevin Bacon game with everyone.

This problem is trying to find the person with the smallest number of Kevin Bacon. The Kevin Bacon number is the sum of the steps that come out when you play the Kevin Bacon game with everyone.

If there are multiple people, print out the person with the smallest number.

Sample Input:
```
5 5
1 3
1 4
4 5
4 3
3 2
```
Sample Output:
```
3
```

### The six degrees of Kevin Bacon
For example, how many steps can Jay of W University and Hajun of B University, who seem to have nothing to do at all, be connected?

Jhon goes to the same school as Jay. Jhon and Emma met through Baekjoon Online Judge. Emma and James founded Startlink together. James and Tom belong to the same school club. Tom and Hajun know each other because they go to the same school. In other words, you only need to go through 5 steps, such as Jay-Jhon-Choi Baek-jun-James-Tom-Hajun.

### BFS: Breadth First Search
The BFS algorithm starts with the initial state and then it visits the neighboring states in a breadth-first manner until the goal state is found or all reachable states are explored.

## Implementation

**Time Complexity:** $\mathcal{O}(N * (N + E)))$
**Space Complexity:** $\mathcal{O{(N + E)$

---
```python
from collections import deque # import deque
import sys # import sys
input = sys.stdin.readline # 
n,m = map(int,input().split())
arr = [[]for i in range(n+1)]
for i in range(m):
    x,y = map(int,input().split())
    arr[x].append(y)
    arr[y].append(x)

def bfs(v):
    visited = [False for _ in range(n+1)]
    v_arr = [0 for _ in range(n+1)]
    cnt = -1
    que = deque([v])
    while len(que) != 0:
        cnt += 1
        for _ in range(len(que)):
            x = que.popleft()
            if not visited[x]:
                visited[x] = True
                v_arr[x] = cnt
                for i in arr[x]:
                    if not visited[i]:que.append(i)
    return sum(v_arr)

value,num = 0,10**8
for i in range(1,n+1):
    k = bfs(i)
    if k < num:num=k;value=i
print(value)
```
