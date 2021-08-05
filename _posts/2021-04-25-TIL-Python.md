---
layout: post
title: "Python"
date: 2021-04-25
categories: TIL argument parameter Python
---

## Parameter / Argument

```
def fuc(a, b, c):
   return a+b+c

fuc(1,2,3)
```

Parameter는 함수가 받는 변수
✔ a,b,c
Argument는 함수에 실제로 들어가는 Input Value
✔ 1,2,3

## value parameter

**default value parameter / non-default value parameter**

```python
def make_value_parameter(a=3, b, c):
  print(a + b)

make_value_parameter(1,2,3)

>> SyntaxError: non-default argument follows default argument
```

무작위로 parameter를 지정하면 정의된 함수가 호출될 때 파이썬은 해당 함수의 parameter가 어떤 값으로 정해졌는지 판단하기가 어렵다
그래서 **parameter의 순서**를 지켜줘야 한다

**parameter를 받는 순서**

```python
def example(a, b, c=None, r="w" , d=[], *ae,  **ab):
```

(a,b) are positional parameter

(c=none) is optional parameter

(r="w") is keyword parameter

(d=[]) is list parameter

(\*ae) is keyword-only
_Tuple 형태로 저장이 된다_

(\*\*ab) is var-keyword parameter
_Dictionaly 형태로 저장이 된다_

---

## Argument Priority

![](https://images.velog.io/images/action2thefuture/post/c772f8e9-d64c-45b8-a847-5542d7921567/parameter%20%EC%9C%84%EC%B9%98.jpg)

```python
def fuc(position, *args, **kwargs):
	...
```

**함수 내의 Argument는 우선순위가 있다**

---

### 1. 위치 인수(positional arguments)와 가변 인수(variable length arguments)

```python
def func_param_with_var_args(name, *args, age):
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("age=",end=""), print(age)

func_param_with_var_args("정우성", "01012341234", "seoul", 20)

>>TypeError: func_param_with_var_args() missing 1 required keyword-only argument: 'age'
```

**\*args로 position argument("정우성") 뒤에 있는 모든 argument를 받아 position parameter(age)를 인식하지 못해 에러가 나타났다**

```python
def mixed_params(age, name="아이유", *args, address, **kwargs):
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("age=",end=""), print(age)
    print("kwargs=",end=""), print(kwargs)
    print("address=",end=""), print(address)

mixed_params(20, "정우성", "01012341234", "male" ,mobile="01012341234", address="seoul")

>>
name='정우성'
args=('01012341234','seoul')
age=20
```

**1. position parameter를 \*args 앞에 정의하여서 해당 위치에 맞게 argument를 수정하거나**

```python
def func_param_with_var_args(name, *args, age):
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("age=",end=""), print(age)

func_param_with_var_args("정우성", "01012341234", "seoul", age=20)

>>
name='정우성'
args=('01012341234','seoul')
age=20
```

**2. age를 Default argument로 정의한다**

---

### 2. 가변 키워드 인수 (variable length keyword arguments)

```python
def func_param_with_kwargs(name, age, **kwargs, address=0):
    print("name=",end=""), print(name)
    print("age=",end=""), print(age)
    print("kwargs=",end=""), print(kwargs)
    print("address=",end=""), print(address)

func_param_with_kwargs("정우성", "20", mobile="01012341234", address="seoul")

>>SyntaxError: invalid syntax
```

**Default Parameter는 가변인수나 키워드인수 앞에 와야 한다
이미 값이 지정된 Default Parameter는 함수를 호출할 때 재정의가 되지 않는 한 그 값으로 고정이 된다**

```python
def func_param_with_kwargs(name, age, address=0, **kwargs):
    print("name=",end=""), print(name)
    print("age=",end=""), print(age)
    print("kwargs=",end=""), print(kwargs)
    print("address=",end=""), print(address)

func_param_with_kwargs("정우성", "20", mobile="01012341234")

>>
name='정우성'
age = 20
args=(mobile="01012341234")
address = 0
```

**default parameter의 위치를 바꿔주니 에러가 해결되었다**

---

### 3. 위치 인수와 키워드 가변 키워드 인수 (variable length keyword arguments)

```python
def mixed_params(name="아이유", *args, age, **kwargs, address):
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("age=",end=""), print(age)
    print("kwargs=",end=""), print(kwargs)
    print("address=",end=""), print(address)

mixed_params(20, "정우성", "01012341234", "male" ,mobile="01012341234", address="seoul")

>>SyntaxError: invalid syntax
```

2번과 비슷한 문제가 발생하였다

```python
def mixed_params(age, name="아이유", *args, address, **kwargs):
    print("name=",end=""), print(name)
    print("args=",end=""), print(args)
    print("age=",end=""), print(age)
    print("kwargs=",end=""), print(kwargs)
    print("address=",end=""), print(address)

mixed_params(20, "정우성", "01012341234", "male" ,mobile="01012341234", address="seoul")

>>
name=정우성
args=('01012341234', 'male')
age=20
kwargs={'mobile': '010123412340'}
address=seoul
```

에러가 해결되었지만 non-default parameter가 default parameter 뒤에 왔지만 파이썬은 이 코드를 받아들였다

**Why❓**
**address라는 non-default parameter이지만 또한 keyword를 받는 argument이다 **
(keyword-only arguments는 default arguments 뒤에 온다)

> https://getkt.com/blog/python-keyword-only-arguments/

---

## Set / Dictionary

set와 dictionary는 비슷하지만 확연한 차이가 존재한다

### 공통점

중복된 값을 가지지 않는다
순서를 가지지 않는다(index로 호출불가)
요소들이 중괄호로 둘러싸여있다

### 차이점

set는 key값만 가질 수 있지만
dictionary는 key값과 value를 함꼐 가진다

**set 정의**

```python
myset = {1,2,3,4,5}
```

**dictionary 정의**

```python
# 중괄호로 정의
mydic = {"a": 1,"b": 2,"c": 3,"d": 4,"e": 5}

# parameter로 정의
mydic = dict(a=1, b=2, c=3, d=4, e=5)
```

## List / Tuple

### 공통점

순서가 있어서 index가 존재한다

### 차이점

List는 대괄호로 둘러싸여 있고 생성되고 변경이 가능하다
Tuple은 소괄호로 둘러싸여 있고 생성되고 변경이 불가능하다
