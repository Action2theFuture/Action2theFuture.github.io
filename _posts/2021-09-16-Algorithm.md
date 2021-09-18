---
layout: post
title: "거의 소수"
date: 2021-09-16
categories: TIL Python Silver1 코딩테스트 백준
---

# [거의 소수](https://www.acmicpc.net/problem/1456)

```python
import sys

a,b = map(int,sys.stdin.readline().split())

answer = 0
for i in range(a,b+1):
  count = 0
  for j in range(1,i+1):
    if i%j == 0:
      count += 1
    if count > 2:
      break
  if count == 2:
    for j in range(2, b+1):
      if b < i**j:
        break
      answer += 1

print(answer)
```

시간 초과
