---
layout: post
title: "쇠막대기"
date: 2021-09-02
categories: TIL Algorithm silver3 백준 코딩테스트 Stack
---

# [쇠막대기](https://www.acmicpc.net/problem/10799)

```python
n = list(input())
stack = []
answer = 0
for i in range(len(n)):
  if n[i] == "(":
    stack.append(n[i])
  else:
    if n[i-1] == "(":
      stack.pop()
      answer += len(stack)
    else:
      stack.pop()
      answer += 1
print(answer)
```
