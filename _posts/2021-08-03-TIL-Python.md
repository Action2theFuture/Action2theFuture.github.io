---
layout: post
title: "Python | Decorator"
date: 2021-08-03
categories: TIL Python Decorator
---

## Decorator

- @으로 시작한다
- 함수는 일급객체이므로 인자로 사용될 수 있다
- 함수가 실행되기 전에 먼저 실행된다
- 또 다른 함수를 반환된다
- 클로저를 이용하여 외부의 인자가 내부로 전달이 된다

**클로저 예시**

```python
def outer(a, b):
  def inner(c):
    return f"{c}이는 {b}로 {a}을 가고싶다"
  return inner

closure = outer("여행", "제주도")
print(closure("운산"))

운산이는 제주도로 여행을 가고싶다
```

### JavaScript의 콜백함수랑 데코레이터의 차이점

- 공통점 : 함수의 인자를 공유한다
- 차이점
  - JavaScript : 함수가 끝나고 다른 함수들이 연속적으로 호출할 경우 사용(비동기적 함수일경우 콜백지옥이 발생하여 함수가 동작이 안될 수 있다)
  - Python : 한 기능을 여러번 사용하기 위해서 사용

**콜백 함수**

```javascript
function add(x) {
  return new Promise((resolve, reject) => {
    let sum = x + x;
    console.log(sum);
    resolve(sum);
  });
}

// 콜백 지옥에 빠질 수 있는 .then()을 사용한 Chaining
add(2).then((result) => {
  add(result).then((result) => {
    add(result).then((result) => {});
  });
});

4;
8;
16;

//async await

const result = async function (x) {
  const add1 = await add(x);
  const add2 = await add(add1);
  const add3 = await add(add2);
  return add4;
};

4;
8;
16;
```

### 데코레이터를 2개이상 연속으로 사용할 시 주의할 점

이중으로 데코레이터를 사용하면 인자값이 중복되서 사용된다

functools의 wraps를 이용하여 중복을 방지할 수 있다

**사용예시**

```python
from functools import wraps

def decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):

        print('전처리1')
        print(func(*args, **kwargs))
        print('후처리1')
    return wrapper


def decorator2(func):
    @wraps(func)
    def wrapper(*args, **kwargs):

        print('전처리2')
        print(func(*args, **kwargs))
        print('후처리2')
    return wrapper

@decorator2
@decorator
def example():
    return '함수'

example()

전처리2
전처리1
함수
후처리1
None
후처리2
```

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        print('전처리1')
        print(func(*args, **kwargs))
        print('후처리1')
        return func()
    return wrapper


def decorator2(func):
    def wrapper(*args, **kwargs):
        print('전처리2')
        print(func(*args, **kwargs))
        print('후처리2')
    return wrapper

@decorator2
@decorator
def example():
    return '함수'

example()

전처리2
전처리1
함수
후처리1
함수
후처리2
```
