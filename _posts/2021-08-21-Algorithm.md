---
layout: post
title: "행렬 테두리 회전하기"
date: 2021-08-21
categories: TIL Algorithm Level2 programmers 코딩테스트 배열회전
---

# [행렬 테두리 회전하기](https://programmers.co.kr/learn/courses/30/lessons/77485)

```python
def solution(rows, columns, queries):
    answer = []
    matrix = [[0 for col in range(columns)] for row in range(rows)]
    number = 1
    for row in range(rows):
        for col in range(columns):
            matrix[row][col] = number
            number += 1

    for t, l, b, r in queries:
        top = t-1
        left = l-1
        bottom = b-1
        right = r-1
        tmp = matrix[top][left]
        minimum = tmp

        for y in range(top, bottom):
            value = matrix[y+1][left]
            matrix[y][left] = value
            minimum = min(minimum, value)

        for x in range(left, right):
            value = matrix[bottom][x+1]
            matrix[bottom][x] = value
            minimum = min(minimum, value)

        for y in range(bottom, top, -1):
            value = matrix[y-1][right]
            matrix[y][right] = value
            minimum = min(minimum, value)

        for x in range(right, left, -1):
            value = matrix[top][x-1]
            matrix[top][x] = value
            minimum = min(minimum, value)

        matrix[top][left+1] = tmp
        answer.append(minimum)

    return answer
```
