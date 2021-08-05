---
layout: post
title: "Stack & Queue"
date: 2021-03-17
categories: TIL Stack&Queue algorithm python DataStructure
---

![](https://images.velog.io/images/action2thefuture/post/e12813da-6c5a-4db6-bb74-d58149bcbe6d/%EC%98%88%EC%8B%9C%2013.jpg)

**Stack : LIFO(Last in First Out)
Queue : FIFO(First in First Out)
Deque : Double ended Queue **

1. Stack
   데이터 넣기 : push
   데이터 꺼내기 : pop

```python
class Stack:
  def __init__(self): # 스택 만들기
    self.stack = []

  def push(self, data): # 데이터 넣기
    self.stack.append(data)

  def pop(self): # 데이터 꺼내기
    if not self.stack:
      return False
    return self.stack.pop() # 마지막에 넣은 데이터를 꺼낸다

  def is_empty(self): # 스택이 비어있는지 확인
    if not self.stack:
      return True     # 비어있으면 True
    else:
      return False    # 비어있지 않으면 False

  def is_contain(self, item): # 스택 안에 해당 요소가 있는지 확인
    return item in self.stack

  def clear(self): # 스택 초기화
    self.stack.clear()

  def peek(self): # 스택에 마지막에 넣은 요소 확인
    self.stack[-1]
```

2. Queue
   데이터 넣기 : EnQueue
   데이터 꺼내기 : DeQueue

```python
class Queue:
  def __init__(self): # 큐만들기
    self.queue = []

  def enqueue(self, data): # 데이터 넣기
    self.queue.append(data)

  def dequeue(self): # 데이터 꺼내기
    if not self.queue:
      return False
    return self.queue.pop(0) # 맨 처음에 넣은 데이터를 꺼낸다

  def is_empty(self): # 큐가 비어있는지 확인
    if not self.queue:
      return True     # 비어있는면 True
    else:
      return False    # 비어있지 않으면 False

  def is_contain(self, item): # 큐 안에 해당 요소가 있는지 확인
    return item in self.queue

  def clear(self): # 큐 초기화
    self.queue.clear()

  def size(self):
  	return len(self.stack)
```

**collections 모듈을 이용하여 Stack과 Queue를 만들 수 있다**

1. Stack

```python
from collections import deque

stack = deque([1,2,3,4,5])

stack.pop()
stack.append('a')
```

2. Queue

```python
from collections import deque

queue = deque([1,2,3,4,5])

# 방향이 왼쪽
queue.popleft()
queue.append('a')

# 방향이 오른쪽
queue. pop()
queue.appendleft('a')
```

3. dequeue

```python
from collections import deque

dequeue = deque([1,2,3,4,5])

dequeue.popleft()
dequeue.appendleft('a')
dequeue.pop()
dequeue.append('b')
```

**💬 복습 **

**Algorithm 문제 풀이 🤪**

> https://programmers.co.kr/learn/courses/30/lessons/42586

**문제 설명**

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

**제한 사항**
작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
작업 진도는 100 미만의 자연수입니다.
작업 속도는 100 이하의 자연수입니다.
배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

**입출력 예**

| progresses               | speeds             | return    |
| ------------------------ | ------------------ | --------- |
| [93, 30, 55]             | [1, 30, 5]         | [2, 1]    |
| [95, 90, 99, 99, 80, 99] | [1, 1, 1, 1, 1, 1] | [1, 3, 2] |

**입출력 예 설명**

**입출력 예 #1**
첫 번째 기능은 93% 완료되어 있고 하루에 1%씩 작업이 가능하므로 7일간 작업 후 배포가 가능합니다.
두 번째 기능은 30%가 완료되어 있고 하루에 30%씩 작업이 가능하므로 3일간 작업 후 배포가 가능합니다. 하지만 이전 첫 번째 기능이 아직 완성된 상태가 아니기 때문에 첫 번째 기능이 배포되는 7일째 배포됩니다.
세 번째 기능은 55%가 완료되어 있고 하루에 5%씩 작업이 가능하므로 9일간 작업 후 배포가 가능합니다.

따라서 7일째에 2개의 기능, 9일째에 1개의 기능이 배포됩니다.

**입출력 예 #2**
모든 기능이 하루에 1%씩 작업이 가능하므로, 작업이 끝나기까지 남은 일수는 각각 5일, 10일, 1일, 1일, 20일, 1일입니다. 어떤 기능이 먼저 완성되었더라도 앞에 있는 모든 기능이 완성되지 않으면 배포가 불가능합니다.

따라서 5일째에 1개의 기능, 10일째에 3개의 기능, 20일째에 2개의 기능이 배포됩니다.

**문제 풀이**

```python
import math

def solution(p, s):
    answer = {}
    for i in range(len(p)):
        answer[i] = (math.ceil((100-p[i])/s[i])) #소수점 이상은 올림
    count = []
    first = 0 #비교할 Index 설정
    for i in range(len(answer)):
        if answer[first] < answer[i]:
            count.append(i-first)
            first = i
    count.append(len(p)-first) #마지막 기능 배포
    return count
```

**다른 사람 풀이**

```python
def solution(progresses, speeds):
    Q=[]
    for p, s in zip(progresses, speeds):
        if len(Q)==0 or Q[-1][0]<-((p-100)//s): #list Q가 빈 list 이거나 앞에 있는 기능이 다 끝났다면
            Q.append([-((p-100)//s),1]) #[걸린 기간, 1]
        else:
            Q[-1][1]+=1 #앞에 기능이 끝나지 않았다면 해당 기능의 수를 더해준다
    return [q[1] for q in Q]
```
