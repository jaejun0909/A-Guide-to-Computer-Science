---
layout: post
author: Hajun Song
tags: [ProblemSolving, BOJ]
---
[Goldbach's Conjecture](https://www.acmicpc.net/problem/6588)
## Explanation

Christian Goldbach, a German amateur mathematician, sent a letter to Leonhard Euler in which he made the following conjecture:
```
Every even number greater than 4 can be written as the sum of two odd prime numbers.
```

For example:
```
8 = 3 + 5. Both 3 and 5 are odd prime numbers.
20 = 3 + 17 = 7 + 13.
42 = 5 + 37 = 11 + 31 = 13 + 29 = 19 + 23.
```
Sample Input:
```
8
20
42
0
```
Sample Output:
```
8 = 3 + 5
20 = 3 + 17
42 = 5 + 37
```

### Sieve of Eratosthenes
The Sieve of Eratosthenes works by iteratively marking the multiples of each prime starting from 2, marking them as non-prime, and continuing this process up to sqrt(n), leaving only the prime numbers unmarked. 
The sieve of Eratosthenes is one of the most efficient ways to find all prime numbers smaller than n when n is smaller than 10 million or so.

## Implementation

**Time Complexity:** O(N)

---
```python
import sys
input = sys.stdin.readline
MAX = 1000001

def solve():
    can = [False]*2+[True]*(MAX-2)
    prime = []
    # Sieve of Eratosthenes
    for i in range(3,int(MAX**0.5),2):
        if can[i]:
            can[i*2::i] = [False]*len(can[i*2::i])

    for i in range(3,MAX,2):
        if can[i]:
            prime.append(i)
    
    n = int(input())
    while n != 0:
        for i in prime:
            if can[n-i]:
                print(f'{n} = {i} + {n-i}')
                break
        n = int(input())
solve()
```
