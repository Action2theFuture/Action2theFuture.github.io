---
layout: post
title: "다리를 지나는 트럭"
date: 2021-08-08
categories: TIL Algorithm Level2 programmers 코딩테스트 stack&queue
---

[다리를 지나는 트럭](https://programmers.co.kr/learn/courses/30/lessons/42583)

```python
from collections import deque

def solution(bridge_length, weight, truck_weights):
    time = 0
    bridge = [0] * bridge_length

    while len(bridge) != 0:
        time += 1
        bridge.pop(0)
        if truck_weights:
            if sum(bridge) + truck_weights[0] <= weight:
                bridge.append(truck_weights.pop(0))
            else:
                bridge.append(0)

    return time
```
