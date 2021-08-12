---
layout: post
title: "합승 택시 요금"
date: 2021-08-12
categories: TIL Algorithm Level3 programmers 코딩테스트 다익스트라알고리즘 Heap
---

**첫번째 풀이**

```python
import heapq

def dijkstra(start, graph, dist):
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
    return dist

def solution(n, s, a, b, fares):
    INF = int(1e9)

    graph = [[] for i in range(n+1)]

    dist = [INF] * (n+1)
    for u, v ,w in fares:
        graph[u].append([v,w])
        graph[v].append([u,w])


    answer = []
    for i in range(1, n+1):
        answer.append(dijkstra(i, graph, dist)[a]+dijkstra(i, graph, dist)[b]+dijkstra(s, graph, dist)[i])


    return answer
```

dist 값이 공유가 되어서 결과값에 영향을 받는 오류가 생긴다

**두번째 풀이**

```python
import heapq

def dijkstra(start, graph , n):
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
    return dist

def solution(n, s, a, b, fares):

    graph = [[] for i in range(n+1)]

    for u, v ,w in fares:
        graph[u].append([v,w])
        graph[v].append([u,w])

    answer = []
    for i in range(1, n+1):
        answer.append(dijkstra(i, graph, n)[a] + dijkstra(i, graph, n)[b] + dijkstra(s, graph, n)[i])

    return min(answer)
```

공유가 되는 인자값을 함수 내에 넣어서 각 함수에 영향을 받지않게 수정
