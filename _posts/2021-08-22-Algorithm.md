---
layout: post
title: "행렬의 곱셈"
date: 2021-08-22
categories: TIL Algorithm Level2 programmers 코딩테스트 행렬
---

# [행렬의 곱셈](https://programmers.co.kr/learn/courses/30/lessons/12949)

```python
def solution(arr1, arr2):

    new_arr2 = list(map(list, zip(*arr2)))

    answer = [[0]*len(arr2[0]) for _ in range(len(arr1))]

    for i in range(len(arr1)):
        for j in range(len(arr2[0])):
            for k in range(len(arr1[0])):
                answer[i][j] += arr1[i][k] * new_arr2[j][k]

    return answer
```

## Test

|  Test  |               arr1                |               arr2                |                   return                   |
| :----: | :-------------------------------: | :-------------------------------: | :----------------------------------------: |
| test 1 |     [[1, 4], [3, 2], [4, 1]]      |         [[3, 3], [3, 3]]          |       [[15, 15], [15, 15], [15, 15]]       |
| test 2 | [[2, 3, 2], [4, 2, 4], [3, 1, 4]] | [[5, 4, 3], [2, 4, 1], [3, 1, 1]] | [[22, 22, 11], [36, 28, 18], [29, 20, 14]] |

### Test 1

| index  | answer |   arr1   |   arr2   |
| :----: | :----: | :------: | :------: |
| (0, 0) |   3    | 1 (0, 0) | 3 (0, 0) |
| (0, 0) |   15   | 4 (0, 1) | 3 (0, 1) |
| (0, 1) |   3    | 1 (0, 0) | 3 (0, 0) |
| (0, 1) |   15   | 4 (0, 1) | 3 (0, 1) |
| (1, 0) |   9    | 3 (1, 0) | 3 (1, 0) |
| (1, 0) |   15   | 2 (1, 1) | 3 (1, 1) |
| (1, 1) |   9    | 3 (1, 0) | 3 (1, 0) |
| (1, 1) |   15   | 2 (1, 1) | 3 (1, 1) |
| (2, 0) |   12   | 4 (2, 0) | 3 (2, 0) |
| (2, 0) |   15   | 1 (2, 1) | 3 (2, 1) |
| (2, 1) |   12   | 4 (2, 0) | 3 (2, 0) |
| (2, 1) |   15   | 1 (2, 1) | 3 (2, 1) |

### Test 2

| index  | answer |   arr1   |   arr2   |
| :----: | :----: | :------: | :------: |
| (0, 0) |   10   | 2 (0, 0) | 5 (0, 0) |
| (0, 0) |   16   | 3 (0, 1) | 2 (0, 1) |
| (0, 0) |   22   | 2 (0, 2) | 3 (0, 2) |
| (0, 1) |   8    | 2 (0, 0) | 4 (0, 0) |
| (0, 1) |   20   | 3 (0, 1) | 4 (0, 1) |
| (0, 1) |   22   | 2 (0, 2) | 1 (0, 2) |
| (0, 2) |   6    | 2 (0, 0) | 3 (0, 0) |
| (0, 2) |   9    | 3 (0, 1) | 1 (0, 1) |
| (0, 2) |   11   | 2 (0, 2) | 1 (0, 2) |
| (1, 0) |   20   | 4 (1, 0) | 5 (1, 0) |
| (1, 0) |   24   | 2 (1, 1) | 2 (1, 1) |
| (1, 0) |   36   | 4 (1, 2) | 3 (1, 2) |
| (1, 1) |   16   | 4 (1, 0) | 4 (1, 0) |
| (1, 1) |   24   | 2 (1, 1) | 4 (1, 1) |
| (1, 1) |   28   | 4 (1, 2) | 1 (1, 2) |
| (1, 2) |   12   | 4 (1, 0) | 3 (1, 0) |
| (1, 2) |   14   | 2 (1, 1) | 1 (1, 1) |
| (1, 2) |   18   | 4 (1, 2) | 1 (1, 2) |
| (2, 0) |   15   | 3 (2, 0) | 5 (2, 0) |
| (2, 0) |   17   | 1 (2, 1) | 2 (2, 1) |
| (2, 0) |   29   | 4 (2, 2) | 3 (2, 2) |
| (2, 1) |   12   | 3 (2, 0) | 4 (2, 0) |
| (2, 1) |   16   | 1 (2, 1) | 4 (2, 1) |
| (2, 1) |   20   | 4 (2, 2) | 1 (2, 2) |
| (2, 2) |   9    | 3 (2, 0) | 3 (2, 0) |
| (2, 2) |   10   | 1 (2, 1) | 1 (2, 1) |
| (2, 2) |   14   | 4 (2, 2) | 1 (2, 2) |

#### 다른 사람 풀이 👀

```python
def solution(arr1, arr2):
    return [[sum(a*b for a, b in zip(A_row,B_col)) for B_col in zip(*arr2)] for A_row in arr1]
```
