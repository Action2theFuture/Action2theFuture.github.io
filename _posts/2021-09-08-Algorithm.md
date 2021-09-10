---
layout: post
title: "Python 입력"
date: 2021-09-08
categories: TIL Python sys
---

### sys.stdin.readline()

- 한 개의 정수를 입력받을 때

```python
import sys
a = int(sys.stdin.readline())
```

- 정해진 개수의 정수를 한줄에 입력받을 때

```python
import sys
a,b,c = map(int,sys.stdin.readline().split())
```

- 임의의 개수의 정수를 한줄에 입력받아 리스트에 저장할 때

```python
import sys
data = list(map(int,sys.stdin.readline().split()))
```

- 임의의 개수의 정수를 n줄 입력받아 2차원 리스트에 저장할 때

```python
import sys
data = []
n = int(sys.stdin.readline())
for i in range(n):
    data.append(list(map(int,sys.stdin.readline().split())))

5
1 2 3
4 5 6
7 8 9
10 11 12
13 14 15

>> [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12], [13, 14, 15]]

```

- 문자열 n줄을 입력받아 리스트에 저장할 때

```python
import sys
n = int(sys.stdin.readline())
data = [sys.stdin.readline().strip() for i in range(n)]

3
나는
세상에서 제일 가는
사람이다

>> ['나는', '세상에서 제일 가는', '사람이다']
```
