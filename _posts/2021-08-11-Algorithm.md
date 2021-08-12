---
layout: post
title: "배달"
date: 2021-08-11
categories: TIL Algorithm Level2 programmers 코딩테스트 다익스트라알고리즘 Heap
---

# [배달](https://programmers.co.kr/learn/courses/30/lessons/12978)

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

테스트 2 실패
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

위 문제풀이에서는 방문한 마을을 방문처리 후 인접한 마을을 방문미처리

아래 문제풀에선 방문한 마을을 방문미처리 후 인접한 마을을 방문처리

해당 노드 상에서 인접한 거리를 계산 후 접근해야겠음

```python
import heapq

def dijkstra(graph, dist):
    Q = []
    heapq.heappush(Q, (0, 1))

    초기값은 자기 자신을 나타내므로 거리비용은 0, 노드 번호는 1

    dist[1] = 0
    자기 자신을 나타내므로 거리비용은 0

    while Q:
        time, node = heapq.heappop(Q)
        힙을 이용하여 시간과 노드값을 꺼낸다

        if dist[node] < time:
            continue
        꺼낸 거리비용이 각 노드에 가는 거리비용보다 작으면 continue

        for i in graph[node]:
            cost = time + i[1]
            각 노드 간의 거리 비용을 계산한다

            if cost < dist[i[0]]:
                dist[i[0]] = cost
                계산한 거리비용이 기존의 거리보다 작을 시 대체한다
                heapq.heappush(Q, (cost, i[0]))
                다시 힙에 집어 넣는다
    return dist

def solution(N, road, K):
    INF = int(1e9)

    graph = [[] for i in range(N+1)]

    마을의 숫자를 대입하기 위해서 범위값을 하나를 더 늘려준다

    인덱스 0은 사용 안한다

    dist = [INF] * (N+1)

    모든 노드의 거리비용은 무한대로 초기값 설정

    for u, v, w in road:
        graph[u].append((v,w))
        graph[v].append((u,w))

    인접한 노득간의 거리비용을 리스트에 대입

    answer = 0
    for i in dijkstra(graph, dist):
        if i <= K:
            answer += 1

    return answer
```

다른 사람 풀이 🙄

```python
import collections
import heapq

def solution(N, road, K):
    graph = collections.defaultdict(list)

    # 인접 리스트 구성
    for u, v, w in road:
        graph[u].append((v,w))
        graph[v].append((u,w))
    # 큐 변수: [(소요 시간, 정점)]
    Q = [(0, 1)]
    dist = collections.defaultdict(int)

    # 우선 순위 큐 최솟값 기준으로 정점까지 최단거리
    while Q:
        time, node = heapq.heappop(Q)
        if node not in dist:
            dist[node] = time
            for v, w in graph[node]:
                alt = time + w
                heapq.heappush(Q,(alt, v))

    answer = 0
    if len(dist) == N:
        for val in dist.values():
            if val <= K:
                answer += 1
    return answer
```
