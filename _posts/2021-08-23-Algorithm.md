---
layout: post
title: "땅따먹기"
date: 2021-08-23
categories: TIL Algorithm Level2 programmers 코딩테스트 2차원배열
---

# [땅따먹기](https://programmers.co.kr/learn/courses/30/lessons/12913)

### 예시

| 1열 | 2열 | 3열 | 4열 |
| :-: | :-: | :-: | :-: |
|  1  |  2  |  3  |  5  |
|  5  |  6  |  7  |  8  |
|  4  |  3  |  2  |  1  |

<br/>

```python
def solution(land):
    for i in range(len(land)-1):
        land[i+1][0] += max(land[i][1],land[i][2],land[i][3])
        land[i+1][1] += max(land[i][0],land[i][2],land[i][3])
        land[i+1][2] += max(land[i][0],land[i][1],land[i][3])
        land[i+1][3] += max(land[i][0],land[i][1],land[i][2])
    return max(land[len(land)-1])

총 4열로 이루어져 있으므로 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 최댓값을 찾는다

```

#### 다른 풀이 👀

```python
import copy

def solution(land):
    result = 0
    # 땅따먹기 게임으로 얻을 수 있는 최대 점수는?
    for i in range(1,len(land)):
        for j in range(4):
            temp = copy.deepcopy(land[i-1])
        copy.deepcopy()를 이용하여 새로운 객체를 만든다
            temp[j] = 0
            land[i][j]+=max(temp)
    result = max(land[-1])
    return result
```

<br/>

|      temp       | land[i][j] |
| :-------------: | :--------: |
|  [0, 2, 3, 5]   |     10     |
|  [1, 0, 3, 5]   |     11     |
|  [1, 2, 0, 5]   |     12     |
|  [1, 2, 3, 0]   |     11     |
| [0, 11, 12, 11] |     16     |
| [10, 0, 12, 11] |     15     |
| [10, 11, 0, 11] |     13     |
| [10, 11, 12, 0] |     13     |

#### 다른 풀이 👀

```python
def solution(land):
    answer = [0]*4
    for i in range(len(land)):
        row = land[i]
        copy = answer[:]
        for j in range(4):
            copy2 = copy[:]
            copy2.pop(j)
            answer[j] = max(copy2)+row[j]
    return max(answer)
```

<br/>

| answer[j] |    copy2     | row[j] |
| :-------: | :----------: | :----: |
|     1     |  [0, 0, 0]   |   1    |
|     2     |  [0, 0, 0]   |   2    |
|     3     |  [0, 0, 0]   |   3    |
|     5     |  [0, 0, 0]   |   5    |
|    10     |  [2, 3, 5]   |   5    |
|    11     |  [1, 3, 5]   |   6    |
|    12     |  [1, 2, 5]   |   7    |
|    11     |  [1, 2, 3]   |   8    |
|    16     | [11, 12, 11] |   4    |
|    15     | [10, 12, 11] |   3    |
|    13     | [10, 11, 11] |   2    |
|    13     | [10, 11, 12] |   1    |
