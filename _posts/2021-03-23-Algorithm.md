---
layout: post
title: "Algorithm🧶 | 위장(Hash)"
date: 2021-03-23
categories: TIL Level2 algorithm hash programmers 코딩테스트
---

> https://programmers.co.kr/learn/courses/30/lessons/42578

**문제 설명**

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.

예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

| 종류 |            이름            |
| :--: | :------------------------: |
| 얼굴 | 동그란 안경, 검정 선글라스 |
| 상의 |       파란색 티셔츠        |
| 하의 |           청바지           |
| 겉옷 |          긴 코트           |

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

**제한사항**

- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '\_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.

**입출력 예**

| clothes                                                                                  | return |
| ---------------------------------------------------------------------------------------- | ------ |
| [["yellowhat", "headgear"], ["bluesunglasses", "eyewear"], ["green_turban", "headgear"]] | 5      |
| [["crowmask", "face"], ["bluesunglasses", "face"], ["smoky_makeup", "face"]]             | 3      |

**입출력 예 설명**

예제 #1
headgear에 해당하는 의상이 yellow_hat, green_turban이고 eyewear에 해당하는 의상이 blue_sunglasses이므로 아래와 같이 5개의 조합이 가능합니다.

```
1. yellow_hat
2. blue_sunglasses
3. green_turban
4. yellow_hat + blue_sunglasses
5. green_turban + blue_sunglasses
```

예제 #2
face에 해당하는 의상이 crow_mask, blue_sunglasses, smoky_makeup이므로 아래와 같이 3개의 조합이 가능합니다.

```
1. crow_mask
2. blue_sunglasses
3. smoky_makeup
```

**문제 풀이**

**첫번째 풀이😁**

```python
def solution(clothes):
    a=0
    two = []
    one = []
    while True:
        if a == len(clothes):
                break
        for i in range(len(clothes)):
            one.append(f"{clothes[i][0]}")
            if i != a and i > a:
                if clothes[a][1] != clothes[i][1]:
                    two.append((clothes[a][0],clothes[i][0]))
            if i == len(clothes)-1:
                    a += 1
    two = list(set(two))
    one = list(set(one))
    return len(two) + len(one)
```

**의상의 종류가 2가지까지의 배열만 만들 수 있다
실패🤪**

**두번째 풀이**

```python
def solution(clothes):
    kind_dic={}
    for name, kind in clothes: #dictionary를 이용하여 각 종류의 갯수를 가지고 온 뒤
        if kind in kind_dic:
            kind_dic[kind] += 1
        else:
            kind_dic[kind] = 1
    count = 1
    for i in kind_dic.values(): #dictionary의 value를 가져와 1을 더한 수를 곱해준다 (1을 더한 이유? 1을 더하지 않으면 해당되는 의상의 종류를 입지않을 경우를 나타내지 못한다)
        count *= i+1
    return count -1 #아무것도 안 입을 경우는 제한다
```

**성공👍**

**다른 사람 풀이 1**

```python
import collections
from functools import reduce

def solution(c):
    return reduce(lambda x,y:x*y,[a+1 for a in collections.Counter([x[1] for x in c]).values()])-1
```

**다른 사람 풀이 2**

```python
def solution(clothes):
    from collections import Counter
    from functools import reduce
    cnt = Counter([kind for name, kind in clothes])
    answer = reduce(lambda x, y: x*(y+1), cnt.values(), 1) - 1
    return answer
```
