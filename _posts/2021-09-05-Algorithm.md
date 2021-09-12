---
layout: post
title: "괄호"
date: 2021-09-05
categories: TIL Algorithm Silver4 백준 코딩테스트 stack
---

# [괄호](https://www.acmicpc.net/problem/9012)

```python
n = int(input())

for _ in range(n):
  stack = []
  a = list(input())
  com = ''
  for i in a:
    if i == "(":
      stack.append(i)
    elif i == ")":
      if not stack:
        print("NO")
        com = "완료"
        break
      else:
        stack.pop()
  if stack and com == '':
    print("NO")
  elif not stack and com == '':
    print("YES")
```
