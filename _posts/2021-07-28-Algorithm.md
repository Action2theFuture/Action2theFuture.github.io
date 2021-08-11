---
layout: post
title: "여행경로"
date: 2021-07-28
categories: TIL Level2 algorithm programmers 코딩테스트 DFS/BFS
---

[여행경로](https://programmers.co.kr/learn/courses/30/lessons/43164)

```python
# BFS풀이

from collections import deque

def bfs(tickets, visited):
    answer = []
    index_list = []
    queue = deque()

    for i in tickets:
        if i[0] == "ICN":
            queue.append(i)
            answer.append(i[0])
            answer.append(i[1])
            visited[tickets.index(i)] = 1
            break

    while queue:
        now, after = queue.popleft()

        for i in range(len(tickets)):
            if visited[i] > 0:
                continue

            if tickets[i][0] == after:
                now, after = tickets[i][0],tickets[i][1]
                queue.append([now, after])
                answer.append(after)
                index_list.append(i)
                visited[i] = 1
                break

    return answer

def solution(tickets):
    visited = [0]*len(tickets)

    tickets.sort(key = lambda tickets : tickets[1])

    return bfs(tickets, visited)

# 실패

# 가까운 경로가 아닌 모든 티켓을 이용해야 하는 경우를 생각하므로 BFS로 구현하기엔 어려움이 있음
# DFS로 접근

```
