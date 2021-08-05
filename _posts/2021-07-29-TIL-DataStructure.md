---
layout: post
title: "트리"
date: 2021-07-29
categories: TIL DataStructure 트리
---

## Tree

**노드로만 이루어진 자료구조(계층적 구조)**

</img src="https://github.com/knotted-developers/Computer-science/blob/8ba6ae3c7911569cca76d940645fda54bd2fb2d6/DataStructure/Images/node.png" width=500 height=300>

### Tree 구성

- 루트 노드 : 최상위 노드
- 단말 노드 : 자식이 없는 노드
- 크기 : 모든 노드의 개수
- 깊이 : 루트 노드로부터의 거리
- 높이 : 깊이 중 최댓값
- 차수 : 자식 노드의 개수
- 간선 : 노드마다 연결된 선

**순회 방식**

1. 전위 순회(preorder traverse) : 뿌리(root)를 먼저 방문
2. 중위 순회(inorder traverse) : 왼쪽 하위 트리를 방문 후 뿌리(root)를 방문
3. 후위 순회(postorder traverse) : 하위 트리 모두 방문 후 뿌리(root)를 방문

- 전위 순회 : A - B - D - H - I - E - J - C - F - G
- 중위 순회 : H - D - I - B - E - J - A - F - C - G
- 후위 순회 : H - I - D - J - E - B - F - G - C - A

### Tree의 특징

- 그래프의 한 종류이다. ‘최소 연결 트리’ 라고도 불린다.
- 트리는 계층 모델 이다.
- 트리는 DAG(Directed Acyclic Graphs, 방향성이 있는 비순환 그래프)의 한 종류이다.
  - loop나 circuit이 없다. 당연히 self-loop도 없다.
  - 즉, 사이클이 없다.
- 노드가 N개인 트리는 항상 N-1개의 간선(edge)을 가진다.
  - 즉, 간선은 항상 (정점의 개수 - 1) 만큼을 가진다.
- 루트에서 어떤 노드로 가는 경로는 유일하다.
  - 임의의 두 노드 간의 경로도 유일하다. 즉, 두 개의 정점 사이에 반드시 1개의 경로만을 가진다.
- 한 개의 루트 노드만이 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가진다.
  - 부모-자식 관계이므로 흐름은 top-bottom 아니면 bottom-top으로 이루어진다.
- 순회는 Pre-order, In-order 아니면 Post-order로 이루어진다. 이 3가지 모두 DFS/BFS 안에 있다.
- 트리는 이진 트리, 이진 탐색 트리, 균형 트리(AVL 트리, red-black 트리), 이진 힙(최대힙, 최소힙) 등이 있다.

</img src="https://github.com/knotted-developers/Computer-science/blob/26ddb5131b21e19b95e4204d75459365243c9df5/DataStructure/Images/%EA%B7%B8%EB%9E%98%ED%94%84%20vs%20%ED%8A%B8%EB%A6%AC.png" width=500 height=300>

### B-Tree

데이터를 정렬하여 탐색, 삽입, 삭제, 순차 접근이 가능하도록 유지하는 트리형 자료구조

- 하나의 노드에 여러 자료가 배치되는 트리구조 이다.
- 만약 한 노드에 M개의 자료가 배치되면 M차 B 트리 라고 명명할 수 있다.

### B-Tree 특징

1. 노드의 자료수가 K 이라면, 자식의 수는 K + 1 개이어야 한다.
2. 자료는 정렬된 상태로 저장된다.
3. 한 노드 N 의 왼쪽 서브트리는 N의 키 작은 값으로 되어 있고, 오른쪽 서브트리는 큰 값으로 되어 있다.
4. ROOT 노드는 적어도 2개 이상의 자식을 가져야한다. ( 트리가 ROOT 노드로만 구성되어있을 경우 예외, 위의 특징 ① 때문에)
5. ROOT 노드를 제외한 모든 노드는 적어도 ⌊ M/2 ⌋ 개의 키를 가지고 있어야 한다. ( ⌊ ⌋ : floor function - 소수점을 버린다.)
   (B 트리의 장점 - 저장 장치의 효율성, 즉 각 노드마다 반 이상 키 값이 저장되어 있다.)
6. 리프노드로 가는 경로의 길이는 모두 같다 = 리프노드는 모두 같은 레벨에 있다.
7. 입력 자료는 중복될 수 없다.

### B-트리의 검색

- 검색은 정말 간단하다. 위에서 언급했듯 이진 탐색을 원하는 키 값을 검색할 수 있다. O(log n)
- 중위 순회를 통한 순차 탐색도 가능한데 이건 성능이 나쁘다.(=> B+ 트리)

### B-트리의 삽입

- 자료는 항상 리프(Leaf) 노드에 추가 된다.
- 리프 노드의 선택은 ROOT 노드부터 시작해 하향식으로 탐색하며 결정한다.
- 선택한 리프 노드에 여유가 있다면 그냥 삽입. 여유가 없다면 분할한다.

### B-트리의 삭제

- 삭제할려는 키 값을 가진 노드가 가지고 있는 키 갯수를 해당 키 값 삭제 후에 M/2 개 이상이 되도록 해야한다.
- 형제한테 빌리기 / 형제와 결합하기 ( 아래서 자세히 설명 )
- 삭제 키가 있는 노드가 내부 노드인 경우 - 대체 키를 찾아 대체한다.( 왼쪽 서브트리 중 가장 큰 값 OR 오른쪽 서브트리 중 가장 작은 값.)

> 출처</br> > https://matice.tistory.com/8</br> > https://darrengwon.tistory.com/874</br>

[B-Tree 구현 사이트](https://www.cs.usfca.edu/~galles/visualization/BTree.html)
