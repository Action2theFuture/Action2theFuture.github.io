---
layout: post
title: "거스름돈"
date: 2021-08-14
categories: TIL Algorithm Level3 programmers 코딩테스트 다이나믹프로그래밍(DP)
---

[거스름돈](https://programmers.co.kr/learn/courses/30/lessons/12907)

```python
from itertools import permutations

def result(n, money):
    result = 0
    for i in money:
        n = divmod(n, i)[1]
    if n == 0:
        result += 1
    return result

def solution(n, money):
    money_list = list(permutations(money, 3))
    answer = 0

    for money in money_list:
        answer += result(n, money)

    return answer
```
