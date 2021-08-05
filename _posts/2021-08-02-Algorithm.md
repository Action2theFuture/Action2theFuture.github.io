---
layout: post
title: "DFS/BFS"
date: 2021-08-02
categories: TIL Algorithm DFS/BFS
---

## DFS

**깊이 우선 탐색(DFS, Depth-First Search)**

- 위에서 아래로 가는 탐색으로 최상단 노드부터 아래로 탐색하는 알고리즘
- 모든 노드를 탐색하기 위해서 사용한다
- 단순 검색 속도에서는 BFS보다는 느리다
- 깊이를 알 수 없는 구조이면 시간이 무한정으로 늘어날 수 있다
- 순환 알고리즘을 이용하므로 python에서는 재귀함수를 이용한다
- 위에서부터 아래로 차례대로 내려오는 구조이므로 스택을 이용하여 구현한다
- 노드를 방문했으면 그 노드를 방문했다는 여부를 검사해야한다

<img src="https://github.com/knotted-developers/Computer-science/blob/e854f1545ebe7ba8c34c6042988565f601885e05/Algorithm/Images/DFS.gif" width="300" height="300">

<details>
<summary>DFS 코드(위 그림 참조)</summary>
<div markdown="1">

```python

graph = [
  [],
  [2,5,9],
  [1,3],
  [2,4],
  [3],
  [1,6,8],
  [5,7],
  [6],
  [5],
  [1,10],
  [9]
]

visited = [False]*11

def dfs(graph, v , visited):
  visited[v] = True
  print(v , end=" ")
  for i in graph[v]:
    if not visited[i]:
      dfs(graph, i, visited)

dfs(graph, 1, visited)

1 2 3 4 5 6 7 8 9 10

```

</div>
</details>
DFS의 시간 복잡도

- DFS는 그래프(정점의 수: N, 간선의 수: E)의 모든 간선을 조회한다.
  - 인접 리스트로 표현된 그래프: O(N+E)
  - 인접 행렬로 표현된 그래프: O(N^2)

## BFS

**너비 우선 탐색(BFS, Breath-First Search)**

- 인접한 노드를 먼저 탐색하는 알고리즘
- 노드 간의 최단 경로 및 임의의 거리를 탐색하기 위해서 사용한다
- DFS보다 구현하기가 복잡하다
- 인접한 노드를 저장하고 꺼내므로 큐를 이용하여 구현한다
- 노드를 방문했으면 그 노드를 방문했다는 여부를 검사해야한다

<img src="https://github.com/knotted-developers/Computer-science/blob/333fa1732df10ece205c737bf4a320bb8cc58cac/Algorithm/Images/BFS.gif" width="300" height="300">

<details>
<summary>BFS 코드(위 그림 참조)</summary>
<div markdown="1">

```python
from collections import deque

graph = [
  [],
  [2,3,4],
  [1,5],
  [1,6,7],
  [1,8],
  [2,9],
  [3,10],
  [3],
  [4],
  [5],
  [6]
]


visited = [False]*11

def bfs(graph, v, visited):
  visited[v] = True
  queue = deque([v])

  while queue:
    v = queue.popleft()
    print(v, end=" ")
    for i in graph[v]:
      if not visited[i]:
        queue.append(i)
        visited[i] = True

bfs(graph, 1, visited)

1 2 3 4 5 6 7 8 9 10
```

</div>
</details>

BFS의 시간 복잡도

- BFS는 그래프(정점의 수: N, 간선의 수: E)
  - 인접 리스트로 표현된 그래프: O(N+E)
  - 인접 행렬로 표현된 그래프: O(N^2)
