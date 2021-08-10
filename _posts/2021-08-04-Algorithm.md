---
layout: post
title: "타겟 넘버"
date: 2021-08-04
categories: TIL Algorithm Level1 programmers 코딩테스트 DFS/BFS
---

[타겟 넘버](https://programmers.co.kr/learn/courses/30/lessons/43165)

```python
def solution(numbers, target):
    answer = 0
    def dfs(n ,idx):
        if idx == len(numbers):
            nonlocal answer
            if n == target:
                answer += 1
        else:
            dfs(n+numbers[idx], idx+1)
            dfs(n-numbers[idx], idx+1)
    dfs(0,0)
    return answer
```
