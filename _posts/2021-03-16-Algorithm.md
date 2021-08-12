---
layout: post
title: "다음 큰 숫자(2진수)"
date: 2021-03-16
categories: 2진수 Level2 algorithm programmers 코딩테스트
---

# [다음 큰 숫자](https://programmers.co.kr/learn/courses/30/lessons/12911)

**문제 설명**

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

**제한 사항**

n은 1,000,000 이하의 자연수 입니다.

**입출력 예**

|  n  | result |
| :-: | :----: |
| 78  |   83   |
| 15  |   23   |

**입출력 예 설명**

**입출력 예#1**

문제 예시와 같습니다.

**입출력 예#2**

15(1111)의 다음 큰 숫자는 23(10111)입니다.

**문제 풀이**

```python
def solution(n):
    bin_number = bin(n)[2:]
    bin_ = "0b1" + bin_number # 예시로 2진수 11001 >> 111001
    for i in range(n+1, int(bin_, 2)+1): # 10진수로 변환하여 범위 설정
        if bin(i)[2:].count("1") == bin_number.count("1"): # 1의 개수가 같으면
            return i  # 해당하는 숫자를 return
            break
```

**다른 사람 풀이**

무한 Loop를 사용

```python
def nextBigNumber(n, count = 0):
    return n if bin(n).count("1") is count else nextBigNumber(n+1, bin(n).count("1") if count is 0 else count)
```

**진수 변환 함수**

2진수 : `bin()` / 0b
8진수 : `oct()` / 0o
16진수 : `hex()` / 0x
10진수 : `int('변환할 숫자','x 진수)`

**format()으로 진수 변환이 가능하다**

`format('변환할 숫자', '진수 값')`

진수 값 : 2(b), 8(o), 10(d), 16(x)
진수 값 앞에 #를 붙이면 접두어 포함이 가능하다

```python
"{0:d}, {0:b}, {0:o}, {0:x}".format(77)

>>> 77, 1001101, 115, 4d
```
