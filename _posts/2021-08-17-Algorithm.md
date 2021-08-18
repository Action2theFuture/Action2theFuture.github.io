---
layout: post
title: "3진법 뒤집기"
date: 2021-08-17
categories: TIL Algorithm Level1 programmers 코딩테스트 n진수
---

# [3진법 뒤집기](https://programmers.co.kr/learn/courses/30/lessons/68935)

### n진수 → 10진수

int() 라는 함수를 사용하여 변환

```python
int(string, base)
```

### 10진수 → 2, 8, 16진수

```python
bin(int) 2진수
oct(int) 8진수
hex(int) 16진수
```

### 10진수 → n진수

```python
def conversion(n, q):
    rev_base = ''

    while n > 0:
        n, mod = divmod(n, q)
        rev_base += str(mod)

    return rev_base[::-1]
```

<br/>

```python

def conversion(n, q):
    rev_base = ''

    while n > 0:
        n, mod = divmod(n, q)
        rev_base += str(mod)

    return rev_base[::-1]

def solution(n):
    return int(conversion(n, 3)[::-1], 3)
```
