---
layout: post
title: "124 나라의 숫자"
date: 2021-08-09
categories: TIL Algorithm Level2 programmers 코딩테스트
---

[124 나라의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12899)

```python
def solution(n):
    if n<=3:
        return '124'[n-1]
    else:
        q, r = divmod(n-1, 3)
        return solution(q) + '124'[r]
```
