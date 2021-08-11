---
layout: post
title: "배달"
date: 2021-08-11
categories: TIL Algorithm Level2 programmers 코딩테스트 DFS/BFS Heap
---

```python
from collections import deque



def solution(N, road, K):

    for i in road:
        if i[0] > i[1]:
            i[0],i[1] = i[1], i[0]

    road = [[i[0]-1,i[1]-1,i[2]] for i in road]
    print(road)
    visited = [0]*N
    visited[0] = 1
    will_visited = [0]*N

    queue = deque()
    queue.append([0, K])
    num = 1

    while queue:
        idx, path = queue.popleft()
        print(idx,path)
        for i in road:
            if idx != 0:
                if visited[idx] == 1:
                    continue

                if path - i[2] < 0:
                    continue


            if i[0] == idx:
                num += 1
                visited[i[0]] = 1
                will_visited[i[1]] = 1
                new_path = path - i[2]
                queue.append([i[1], new_path])

    return num
테스트 1 통과
```

```python
from collections import deque



def solution(N, road, K):

    for i in road:
        if i[0] > i[1]:
            i[0],i[1] = i[1], i[0]

    road = [[i[0]-1,i[1]-1,i[2]] for i in road]
    print(road)
    visited = [0]*N
    visited[0] = 1
    will_visited = [0]*N

    queue = deque()
    queue.append([0, K])
    num = 1

    while queue:
        idx, path = queue.popleft()
        print(idx,path)
        for i in road:
            if idx != 0:
                if visited[idx] == 1:
                    continue

                if path - i[2] < 0:
                    continue

            if path - i[2] == 0 and will_visited[idx] == 1:
                continue

            if i[0] == idx:
                num += 1
                visited[i[0]] = 1
                will_visited[i[1]] = 1
                new_path = path - i[2]
                queue.append([i[1], new_path])

    return num
테스트 2 통과
```
