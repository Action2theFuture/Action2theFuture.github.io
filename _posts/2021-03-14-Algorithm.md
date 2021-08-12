---
layout: post
title: "시저 암호(find함수, ASCII Code)"
date: 2021-03-14
categories: Level1 programmers 정규표현식 코딩테스트
---

전에 풀었던 문제지만 정규표현식을 복습한다는 생각으로 다시 풀어보았다

# [시저 암호](https://programmers.co.kr/learn/courses/30/lessons/12926)

**문제 설명**

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

**제한 조건**

공백은 아무리 밀어도 공백입니다.
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
s의 길이는 8000이하입니다.
n은 1 이상, 25이하인 자연수입니다.

**입출력**

|    s    |  n  | result  |
| :-----: | :-: | :-----: |
|  "AB"   |  1  |  "BC"   |
|   "z"   |  1  |   "a"   |
| "a B z" |  4  | "e F d" |

**첫 문제풀이**

```python
def solution(s, n):
    Alpa = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    alpa = "abcdefghijklmnopqrstuvwxyz"
    answer = ""
    for i in s:
        if i == " ":
            answer += i
        elif i != " ":
            for j in range(len(Alpa)):
                if i == Alpa[j]:
                    if j+1 >= len(Alpa):
                        answer += Alpa[n-1]
                    elif j+n < len(Alpa):
                        answer += Alpa[j+n]
                elif i == alpa[j]:
                    if j+1 >= len(Alpa):
                        answer += alpa[n-1]
                    elif j+n < len(Alpa):
                        answer += alpa[j+n]
    return answer
```

**3개의 테스트 통과
채점은 실패🙄**

**👍성공**

```python
def solution(s, n):
    Alpa = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    alpa = "abcdefghijklmnopqrstuvwxyz"
    answer = ""
    for i in s:
        if i in Alpa:
            number = Alpa.find(i)+n
            answer += Alpa[number%26]
        elif i in alpa:
            number = alpa.find(i)+n
            answer += alpa[number%26]
        elif i == " ":
            answer += i
    return answer
```

**다른 사람 풀이**

👇find 함수를 이용하여 구한다

```python
def solution(s, n):
    Alpa = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    alpa = "abcdefghijklmnopqrstuvwxyz"
    answer = ""
    for i in s:
        if i in Alpa:
            number = Alpa.find(i)+n
            answer += Alpa[number%26]
        elif i in alpa:
            number = alpa.find(i)+n
            answer += alpa[number%26]
        elif i == " ":
            answer += i
    return answer
```

👇ASCII code를 이용

```python
def caesar(s, n):
    s = list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i]=chr((ord(s[i])-ord('A')+ n)%26+ord('A'))
        elif s[i].islower():
            s[i]=chr((ord(s[i])-ord('a')+ n)%26+ord('a'))

    return "".join(s)
```

**ASCII code**

chr() : 아스키 코드에서 해당되는 문자열을 가져온다

ord() : 아스키 코드값을 돌려준다

[아스키 코드](https://ko.wikipedia.org/wiki/ASCII)

**ASCII code 10진법**

| 코드 값 | 해당 문자열 |
| :-----: | :---------: |
|  48~57  |    [0-9]    |
|  65~90  |    [A-Z]    |
| 97~122  |    [a-z]    |
