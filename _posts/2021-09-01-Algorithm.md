---
layout: post
title: "탑"
date: 2021-09-01
categories: TIL Algorithm Gold5 백준 코딩테스트 Stack
---

# [탑](https://www.acmicpc.net/problem/2493)

```python
n = int(input())
top = list(map(int, input().split()))
stack = []
answer = []

for i in range(n):
  while stack:
      if stack[-1][1] > top[i]:
        answer.append(stack[-1][0] + 1)
        break
      stack.pop()
  if not stack:
    answer.append(0)

  stack.append([i, top[i]])

for i in range(n):
  print(answer[i], end = " ")
```
