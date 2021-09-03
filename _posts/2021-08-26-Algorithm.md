---
layout: post
title: "단어 정렬"
date: 2021-08-26
categories: TIL Algorithm Silver5 백준 코딩테스트 정렬
---

# [단어 정렬](https://www.acmicpc.net/problem/1181)

```python
import sys

n = int(sys.stdin.readline())
data = [sys.stdin.readline().strip() for i in range(n)]
data = list(set(data))
data = list(zip([len(x) for x in data], data))
data.sort()

for i, j in data:
  print(j)
```
