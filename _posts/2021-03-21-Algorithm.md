---
layout: post
title: "전화번호 목록(Hash)"
date: 2021-03-21
categories: TIL Level2 algorithm hash programmers 코딩테스트
---

# [전화번호 목록](https://programmers.co.kr/learn/courses/30/lessons/42577)

**문제 설명**
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

**제한 사항**

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
  - 각 전화번호의 길이는 1 이상 20 이하입니다.
  - 같은 전화번호가 중복해서 들어있지 않습니다.

**입출력 예제**

| phone_book                        | return |
| --------------------------------- | ------ |
| ["119", "97674223", "1195524421"] | false  |
| ["123","456","789"]               | true   |
| ["12","123","1235","567","88"]    | false  |

**입출력 예 설명**

**입출력 예 #1**
앞에서 설명한 예와 같습니다.

**입출력 예 #2**
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

**입출력 예 #3**
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

알림

2021년 3월 4일, 테스트 케이스가 변경되었습니다. 이로 인해 이전에 통과하던 코드가 더 이상 통과하지 않을 수 있습니다.

**문제 풀이**

```python
def solution(p):
    p.sort()
    number = 0
    answer = True
    for i in range(len(p)):
        for j in range(i+1, len(p)):
            if i != j:
                if p[i] == p[j][:len(p[i])]:
                    return False
    return answer

```

효율성 테스트 3,4 실패🥴

**다른 사람 풀이**

```python
def solution(phone_book):
    answer = True
    hash_map = {}
    for phone_number in phone_book:
        hash_map[phone_number] = 1
    for phone_number in phone_book:
        temp = ""
        for number in phone_number:
            temp += number
            if temp in hash_map and temp != phone_number:
                answer = False
    return answer
```
