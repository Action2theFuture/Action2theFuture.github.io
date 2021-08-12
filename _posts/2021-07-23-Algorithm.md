---
layout: post
title: "거리두기 확인하기"
date: 2021-07-23
categories: TIL Level2 algorithm programmers 코딩테스트
---

# [거리두기 확인하기](https://programmers.co.kr/learn/courses/30/lessons/81302)

```python
from collections import deque

def bfs(x, y, room):

    queue = deque()
    queue.append([x, y])

    dx = [-1,1,0,0]
    dy = [0,0,-1,1]

    visited = [[0]*5 for _ in range(5)]
    distance = [[0]*5 for _ in range(5)]
    visited[x][y] = 1

    while queue:
        x, y = queue.popleft()

        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]

            if 0 > nx or nx >= 5:
                continue

            if ny < 0 or ny >= 5:
                continue

            if visited[nx][ny] > 0:
                continue
            # 좌표 범위를 넘어가지 않고 인접한 좌표가 방문하지 않으면

            if room[nx][ny] == "O":
                visited[nx][ny] = 1
                #방문 확인
                distance[nx][ny] = distance[x][y] +1
                #거리 측정
                queue.append([nx,ny])
                #큐에 다음 수행할 좌표 넣기

            if room[nx][ny] == "P" and distance[x][y] < 2:
                # 인접한 사람이 있고 거리가 2보다 작으면
                return False
    return True

def solution(places):
    answer = [1]*5
    index = 0
    for room in places:
        for x in range(5):
            for y in range(5):
                if room[x][y] == "P":
                    if not bfs(x , y, room):
                        answer[index] = 0
        index += 1

    return answer
```
