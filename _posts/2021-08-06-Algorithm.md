---
layout: post
title: "기능 개발"
date: 2021-08-06
categories: TIL Algorithm Level2 programmers 코딩테스트
---

[기능 개발](https://programmers.co.kr/learn/courses/30/lessons/42586)

```python
import math

def solution(p, s):
    answer = {}
    for i in range(len(p)):
        answer[i] = (math.ceil((100-p[i])/s[i])) #소수점 이상은 올림
    count = []
    first = 0 #비교할 Index 설정
    for i in range(len(answer)):
        if answer[first] < answer[i]:
            count.append(i-first)
            first = i
    count.append(len(p)-first) #마지막 기능 배포
    return count
```

## 다른 사람 풀이

```python
def solution(progresses, speeds):
    Q=[]
    for p, s in zip(progresses, speeds):
        if len(Q)==0 or Q[-1][0]<-((p-100)//s): #list Q가 빈 list 이거나 앞에 있는 기능이 다 끝났다면
            Q.append([-((p-100)//s),1]) #[걸린 기간, 1]
        else:
            Q[-1][1]+=1 #앞에 기능이 끝나지 않았다면 해당 기능의 수를 더해준다
    return [q[1] for q in Q]
```
