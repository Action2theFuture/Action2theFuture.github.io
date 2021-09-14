---
layout: post
title: "Python | Numpy2"
date: 2021-09-14
categories: TIL Python Silver3 백준 코딩테스트 이진탐색
---

# [랜선 자르기](https://www.acmicpc.net/problem/1654)

```python
import sys

n, number = map(int, sys.stdin.readline().split())
data = [int(sys.stdin.readline().strip()) for i in range(n)]

start, end = 1, max(data)


while start <= end:
    mid = (start+end)//2

    lines = 0
    for i in data:
        lines += i//mid

    if lines >= number:
        start = mid+1
    else:
        end = mid-1

print(end)
```

**예제**

```
입력
4 11
802
743
457
539
```

| Start | Mid | End | Lines |
| :---: | :-: | :-: | :---: |
|   1   | 401 | 802 |   5   |
|   1   | 200 | 400 |  11   |
|  201  | 300 | 400 |   6   |
|  201  | 250 | 299 |   8   |
|  201  | 225 | 249 |  10   |
|  201  | 212 | 224 |  10   |
|  201  | 206 | 221 |  10   |
|  201  | 203 | 205 |  10   |
|  201  | 201 | 202 |  10   |
|  201  |     | 200 |  10   |

```
출력

200
```
