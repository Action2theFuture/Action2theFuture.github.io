---
layout: post
title: "Lambda"
date: 2021-07-17
categories: TIL Lambda
---

</br>
</br>
</br>
# Lambda

**메소드를 하나의 표현식으로 나타낸 것**

- 함수형 프로그래밍이 각광받고 있는 요즘 여러 클래스를 나눌 필요없이 하나의 함수안에 람다표현식으로 간결하게 나타낼 수 있다

- 불필요한 Loop문을 줄일 수 있다

- 표현식만으로 return값을 되돌려준다

## 정렬

```python
def check_password(password):
    if len(password) < 8:
        return 'SHORT_PASSWORD'

    if not any(c.isupper() for c in password):
        return 'NO_CAPITAL_LETTER_PASSWORD'

    return True

# Lambda형 변환

lambdas = [
  lambda x : 'SHORT_PASSWORD' if len(x) < 8 else None,
  lambda x : 'NO_CAPITAL_LETTER_PASSWORD' if not any(c.isupper() for c in x) else None
]

def check_password_using_lambda(password):

    for f in lambdas:
        if f(password) is not None:
            return f(password)

    return True


print( check_password_using_lambda('123') )
# SHORT_PASSWORD
print( check_password_using_lambda('12356789f') )
# NO_CAPITAL_LETTER_PASSWORD
print( check_password_using_lambda('123456789F') )
# True
```

### any()

**전달받은 자료형의 element 중 하나라도 True일 경우 True를 돌려준다.
(만약 empty 값을 argument로 넘겨주었다면 False를 돌려준다.)**

## map

** list(map(lambda x: x , list )**
**각 리스트 요소들을 x의 상태값으로 바꾸어 새로운 객체를 리턴한다**'

```python
def solution(numbers):
    numbers = list(map(str, numbers))
    numbers.sort(key = lambda x: x*3, reverse=True)
    return str(int("".join(numbers)))
```

## filter

**filter 조건의 boolean 값이 True 참인 요소만 반환한다**

```python
numberList = [1, 2, 3, 4, 5]
result = list(filter(lambda x : int == type(x), numberList))

# [1, 2, 3, 4, 5]
```

## Reduce

**functools에 있는 모듈로 앞에서부터 차례대로 계산을 해준다**

```python
from functools import reduce

list = [ 1, 2, 3, 4, 5]

def addList(list):
  return reduce(lambda x, y : x + y, list)

# 15
```

##
