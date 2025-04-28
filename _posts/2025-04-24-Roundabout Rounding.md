---
layout: post
author: Jaehun Jang
tags: [ProblemSolving , USACO-Bronze]
---

[USACO Bronze 2024 December](https://usaco.org/index.php?page=viewproblem2cpid=1443)
    

## Explanation
The question is:
There are two ways to round a number. One is to just round it 
and the other is to round it from the very beginning one by one.
For example, 
445 can be rounded to 400 if you just round it,
but 445 can first be rounded to 450 and then to 500

We need to calculate how many integers between 1 to N have different values when we did both of the rounding.

The input is like:
```
T (the number of test cases)
N 
N
(on and on)
```
The output is like
```
awnsers for every test case
awnsers for every test case
awnsers for every test case
(on and on)
```

For example, let's look at the sample input:

```
4
1
100
4567
3366
```

The output is 
```
0
5
183
60
```

We need to look at the number 4 which brings a difference. 
4, 40+n(5~9),400+n(50~99)
can bring differences.

## Implementation

a if the maximum number of digits\
n is the maximum value of n encountered across all test cases.\
**Time Complexity:** $\mathcal{O}(a)$  
**Space Complexity:** $\mathcal{O}(T*a + n)$

```py
#input
from sys import stdin,stdout,setrecursionlimit
input = stdin.readline
print = stdout.write
setrecursionlimit(10**7)

#count the 5s 
mem = [0,0,5]
def f(n):
    if len(mem)-1 >= n: return mem[n]
    for i in range(len(mem),n+1):
        mem.append(mem[-1]+int('5'*(i-1)))
    return mem[n]

#each test case
for _ in range(int(input())):
    n = input()
    a = len(n)
    ni = int(n)
    
    #calculate
    if ni >= 5*10**(a-2): print(str(f(a-1))+'\n')
    elif ni <= int('4'*(a-1)): print(str(f(a-2))+'\n')
    else: 
        cnt = f(a-2)
        for i in range(a-1):
            if int(n[i]) >= 5: 
                cnt += int('5'*(a-i-2) if a-i-2 > 0 else 0)+ -5*10**(len(n[i:])-2)+int(n[i:])+1
                break
        print(str(cnt)+'\n')
```

