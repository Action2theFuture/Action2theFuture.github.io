---
layout: post
title: "비밀지도"
date: 2021-08-05
categories: TIL Algorithm Level1 programmers 코딩테스트
---

# [비밀지도](https://programmers.co.kr/learn/courses/30/lessons/17681)

```python
def solution(n, arr1, arr2):
    answer = []
    for a1, a2 in zip(arr1,arr2):
        a = str(bin(a1|a2))[2:]
        a = '0' * (n - len(a)) + a
        a = a.replace("1","#")
        a = a.replace("0"," ")
        answer.append(a)
    return answer
```
