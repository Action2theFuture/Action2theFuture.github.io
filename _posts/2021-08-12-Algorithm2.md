---
layout: post
title: "외벽 점검"
date: 2021-08-13
categories: TIL Algorithm Level3 programmers 코딩테스트 다익스트라알고리즘 Heap
---

```python
from itertools import permutations
import heapq

def dijkstra(start, graph, n):
    INF = int(1e9)

    dist = [INF] * (n+1)

    q = []
    heapq.heappush(q, (0, start))

    dist[start] = 0

    while q:
        fare, node = heapq.heappop(q)

        if dist[node] < fare:
            continue

        for i in graph[node]:
            cost = fare + i[1]

            if cost < dist[i[0]]:
                dist[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

    return [i for i in dist if i != INF]

def solution(n, weak, dist):

    graph = [[] for i in range(n+1)]

    p = list(permutations(weak, 2))
    for i,j in p:
        if i > j:
            if i-j > 6:
                graph[i].append([j, 12-(i-j)])
            else:
                graph[i].append([j, i-j])
        if i < j:
            if j-i > 6:
                graph[i].append([j, 12-(j-i)])
            else:
                graph[i].append([j, j-i])
    return p
    result = []
    for start in weak:
        result.append(max(dijkstra(start, graph, n)))

    dist.sort(reverse=True)
    tmp = min(result)

    answer = 1
    for i in dist:
        if i >= tmp:
            break
        if i < tmp:
            answer += 1
            tmp -= i

    return answer
```
