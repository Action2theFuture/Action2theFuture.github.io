---
layout: post
title: "입실 퇴실"
date: 2021-09-25
categories: TIL Python Programmers Level2 Stack
---

# [입실 퇴실](https://programmers.co.kr/learn/courses/30/lessons/86048)

```python
from collections import deque

def solution(enter, leave):
    answer = [0]*(len(enter)+1)
    leave = deque(leave)

    room = []
    for i in enter:
        for r in room:
            answer[r] += 1

        answer[i] += len(room)
        room.append(i)
        print(i,answer, room)

        while leave and leave[0] in room:
            room.remove(leave.popleft())

    return answer[1:]
```

입력값 〉 [1, 4, 2, 3], [2, 1, 3, 4]  
기댓값 〉 [2, 2, 1, 3]

|  i  |     answer      |   room    |
| :-: | :-------------: | :-------: |
|  1  | [0, 0, 0, 0, 0] |    [1]    |
|  4  | [0, 1, 0, 0, 1] |  [1, 4]   |
|  2  | [0, 2, 2, 0, 2] | [1, 4, 2] |
|  3  | [0, 2, 2, 1, 3] |  [4, 3]   |

입력값 〉 [1, 4, 2, 3], [2, 1, 4, 3]  
기댓값 〉 [2, 2, 0, 2]

|  i  |     answer      |   room    |
| :-: | :-------------: | :-------: |
|  1  | [0, 0, 0, 0, 0] |    [1]    |
|  4  | [0, 1, 0, 0, 1] |  [1, 4]   |
|  2  | [0, 2, 2, 0, 2] | [1, 4, 2] |
|  3  | [0, 2, 2, 0, 2] |    [3]    |

## 문제 풀이

입실자와 퇴실자의 관계를 찾기위해서 생각을 해보았지만 더욱 복잡하게 만드는 과정이었다  
방안의 사람들이 모여있으면 그 사람들은 필연적으로 만난 사람들이다

answer 리스트는 인덱스가 사람 명부에 적힌 번호이다  
stack을 사용하여 해당 되는 번호가 방에 들어가기전에 room안의 요소의 개수를 answer 인덱스에 더해준다  
그다음 퇴실자를 제외를 시킨다(room의 번호, leave 맨 앞 요소 제거)
