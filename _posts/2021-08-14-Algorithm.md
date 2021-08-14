---
layout: post
title: "거스름돈"
date: 2021-08-14
categories: TIL Algorithm Level3 programmers 코딩테스트 다이나믹프로그래밍(DP)
---

[거스름돈](https://programmers.co.kr/learn/courses/30/lessons/12907)

```python
from itertools import permutations

def result(n, money):
    result = 0
    for i in money:
        n = divmod(n, i)[1]
    if n == 0:
        result += 1
    return result

def solution(n, money):
    money_list = list(permutations(money, 3))
    answer = 0

    for money in money_list:
        answer += result(n, money)

    return answer
```

```python
def solution(n, money):

    d = [0]*(n+1)
    d[0] = 1

    for i in money:
        for j in range(i, n+1):
        보유하고있는 돈부터 거슬러야되는 돈까지 범위설정
            d[j] += d[j-i]

    return d[n]
```

### 반복문이 돌면서 계산되는 값

**각 열은 거슬러 줘야하는 돈을 나타낸다**

**초기값 설정**

|  0  |  1  |  2  |  3  |  4  |  5  |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  1  |  0  |  0  |  0  |  0  |  0  |

**가지고있는 돈이 1**

|  0  |  1  |  2  |  3  |  4  |  5  |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  1  |  1  |  1  |  1  |  1  |  1  |

**가지고있는 돈이 1,2**

|  0  |  1  |  2  |  3  |  4  |  5  |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  1  |  1  |  2  |  2  |  3  |  3  |

**가지고있는 돈이 1,2,5**

|  0  |  1  |  2  |  3  |  4  |  5  |
| :-: | :-: | :-: | :-: | :-: | :-: |
|  1  |  1  |  2  |  2  |  3  |  4  |
