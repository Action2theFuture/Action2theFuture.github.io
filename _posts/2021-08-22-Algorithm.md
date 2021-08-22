---
layout: post
title: "행렬의 곱셈"
date: 2021-08-21
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

|  test  |               arr1                |               arr2                |                   return                   |
| :----: | :-------------------------------: | :-------------------------------: | :----------------------------------------: |
| test 1 |     [[1, 4], [3, 2], [4, 1]]      |         [[3, 3], [3, 3]]          |       [[15, 15], [15, 15], [15, 15]]       |
| test 2 | [[2, 3, 2], [4, 2, 4], [3, 1, 4]] | [[5, 4, 3], [2, 4, 1], [3, 1, 1]] | [[22, 22, 11], [36, 28, 18], [29, 20, 14]] |

answer : 3 (0, 0) arr1 : 1 (0, 0) new_arr2 : 3 (0, 0)
answer : 15 (0, 0) arr1 : 4 (0, 1) new_arr2 : 3 (0, 1)
answer : 3 (0, 1) arr1 : 1 (0, 0) new_arr2 : 3 (0, 0)
answer : 15 (0, 1) arr1 : 4 (0, 1) new_arr2 : 3 (0, 1)
answer : 9 (1, 0) arr1 : 3 (1, 0) new_arr2 : 3 (1, 0)
answer : 15 (1, 0) arr1 : 2 (1, 1) new_arr2 : 3 (1, 1)
answer : 9 (1, 1) arr1 : 3 (1, 0) new_arr2 : 3 (1, 0)
answer : 15 (1, 1) arr1 : 2 (1, 1) new_arr2 : 3 (1, 1)
answer : 12 (2, 0) arr1 : 4 (2, 0) new_arr2 : 3 (2, 0)
answer : 15 (2, 0) arr1 : 1 (2, 1) new_arr2 : 3 (2, 1)
answer : 12 (2, 1) arr1 : 4 (2, 0) new_arr2 : 3 (2, 0)
answer : 15 (2, 1) arr1 : 1 (2, 1) new_arr2 : 3 (2, 1)

#### 다른 사람 풀이 👀

```python
def solution(arr1, arr2):
    return [[sum(a*b for a, b in zip(A_row,B_col)) for B_col in zip(*arr2)] for A_row in arr1]
```
