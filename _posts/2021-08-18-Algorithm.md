---
layout: post
title: "체육복"
date: 2021-08-18
categories: TIL Algorithm Level1 programmers 코딩테스트 탐욕법 Greedy
---

[체육복](https://programmers.co.kr/learn/courses/30/lessons/42862)

### 집합

```python
합집합
lst1 = ['A', 'B', 'C', 'D']
lst2 = ['C', 'D', 'E', 'F']
union = list(set(lst1) | set(lst2))
['D', 'F', 'E', 'B', 'A', 'C']
union = list(set().union(lst1,lst2))
['D', 'F', 'E', 'B', 'A', 'C']

교집합
intersection = list(set(lst1) & set(lst2))
['C', 'D']
intersection = list(set(lst1).intersection(lst2))
['C', 'D']

차집합
complement = list(set(lst1) - set(lst2))
['A', 'B']
complement = list(set(lst1).difference(lst2))
['B', 'A']

대칭 차집합
sym_diff = list(set(lst1) ^ set(lst2))
['A', 'E', 'B', 'F']
sym_diff = list(set(lst1).symmetric_difference(lst2))
['A', 'E', 'B', 'F']
```

```python
def solution(n, lost, reserve):
    new_reserve = list(set(reserve).difference(lost))
    new_lost = list(set(lost).difference(reserve))
    for i in new_reserve:
        if i - 1 in new_lost:
            new_lost.remove(i-1)
        elif i + 1 in new_lost:
            new_lost.remove(i+1)
    return n - len(new_lost)
```
