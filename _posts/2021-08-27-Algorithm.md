---
layout: post
title: "요세푸스 문제 0"
date: 2021-08-27
categories: TIL Algorithm Silver4 백준 코딩테스트 Queue
---

```python
import sys

n, m = map(int, sys.stdin.readline().split())
data = [i for i  in range(1, n+1)]
num = m - 1
answer = []

while data:
    if num >= len(data):
        num = num % len(data)
    else:
        answer.append(str(data.pop(num)))
        num += (m-1)

print("<", ", ".join(answer), ">", sep='')
```

과정

|                data |           num           | answer                |
| ------------------: | :---------------------: | :-------------------- |
| 1, 2, 3, 4, 5, 6, 7 |            2            | [3]                   |
|    1, 2, 4, 5, 6, 7 |            4            | [3, 6]                |
|       1, 2, 4, 5, 7 |      6 >> 6%5 = 1       | [3, 6, 2]             |
|          1, 4, 5, 7 |            3            | [3, 6, 2, 7]          |
|             1, 4, 6 |      5 >> 5%3 = 2       | [3, 6, 2, 7, 5]       |
|                1, 4 | 4 >> 4%2 = 0 | [3, 6, 2, 7, 5, 1]    |
|                   4 | 2 >> 2%1 = 1 >> 1%1 = 0 | [3, 6, 2, 7, 5, 1 ,4] |
