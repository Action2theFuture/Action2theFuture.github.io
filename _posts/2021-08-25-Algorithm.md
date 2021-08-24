---
layout: post
title: "체스판 다시 칠하기"
date: 2021-08-25
categories: TIL Algorithm Silver5 백준 코딩테스트 완전탐색 브루탈포스 매트릭스탐색
---

# [체스판 다시 칠하기](https://www.acmicpc.net/problem/1018)

```python
import sys

row, col = map(int,sys.stdin.readline().split())

matrix = [sys.stdin.readline().strip() for i in range(row)]

def check(slice_mat):
  num_W = 0
  num_B = 0
  for i in range(8):
    for j in range(8):
      if (i+j) % 2 != 0:
    각 인덱스의 합으로 홀짝 구분
        if slice_mat[i][j] != 'B':
          num_W += 1
        if slice_mat[i][j] != 'W':
          num_B += 1
      else:
        if slice_mat[i][j] != 'W':
          num_W += 1
        if slice_mat[i][j] != 'B':
          num_B += 1
  return min(num_W, num_B)

min_num = float('INF')
for i in range(row-7):
  for j in range(col-7):
    slice_mat = [row[j:j+8] for row in matrix[i:i+8]]
    min_num = min(min_num, check(slice_mat))
print(min_num)
```

#### 인덱스

|     |  1열  |  2열  |  3열  |  4열  |
| :-: | :---: | :---: | :---: | :---: |
| 1행 | (0,0) | (0,1) | (0,2) | (0,3) |
| 2행 | (1,0) | (1,1) | (1,2) | (1,3) |
| 3행 | (2,0) | (2,1) | (2,2) | (2,3) |
| 4행 | (3,0) | (3,1) | (3,2) | (3,3) |

#### 체스판

|     |  1열  |  2열  |  3열  |  4열  |
| :-: | :---: | :---: | :---: | :---: |
| 1행 | 0(짝) | 1(홀) | 2(짝) | 3(홀) |
| 2행 | 1(홀) | 2(짝) | 3(홀) | 4(짝) |
| 3행 | 2(짝) | 3(홀) | 4(짝) | 5(홀) |
| 4행 | 3(홀) | 4(짝) | 5(홀) | 6(짝) |
