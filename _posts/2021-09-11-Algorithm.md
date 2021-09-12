---
layout: post
title: "색종이 만들기"
date: 2021-09-11
categories: TIL Algorithm Silver3 백준 코딩테스트
---

# [색종이 만들기](https://www.acmicpc.net/problem/2630)

```python
import sys, itertools

data = []
n = int(sys.stdin.readline())
for i in range(n):
    data.append(list(map(int,sys.stdin.readline().split())))

white = 0
blue = 0
def invest_func(data):
  global white
  global blue
  if sum(itertools.chain(*data)) == 0:
    white += 1
  elif sum(itertools.chain(*data)) == len(list(itertools.chain(*data))):
    blue += 1
  else:
    solution(data, len(data))

def solution(data, n):

  if sum(itertools.chain(*data)) == 0 or sum(itertools.chain(*data)) == len(list(itertools.chain(*data))):
    invest_func(data)
  else:
    cut_list1 = [i[:n//2] for i in data[:n//2]] #좌상
    cut_list2 = [i[n//2:] for i in data[:n//2]] #우상
    cut_list3 = [i[:n//2] for i in data[n//2:]] #좌하
    cut_list4 = [i[n//2:] for i in data[n//2:]] #우하

    invest_func(cut_list1)
    invest_func(cut_list2)
    invest_func(cut_list3)
    invest_func(cut_list4)

solution(data,n)
print(white)
print(blue)
```
