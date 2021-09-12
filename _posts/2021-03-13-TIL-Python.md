---
layout: post
title: "Python | func, class"
date: 2021-03-13
categories: TIL Python Function class generator
---

## 파이썬(Python)

---

![](https://images.velog.io/images/action2thefuture/post/4279098b-105f-4a24-9a14-bb77d9f3373b/python.png)

1991년에 프로그래머인 귀도 반 로섬(Guido van Rossum)이 발표한 프로그래밍언어로 간결하고 쉬운 문법으로 인기있는 프로그래밍 언어 중 하나이다

> "Life is too short, You need python."

Python의 이름은 비단뱀을 뜻한다 그래서 Python을 사용하다보면 뱀과 관련된 이름들이 많다

### Python Rule

**사용자끼리 혼란을 줄이기 위해 서로간의 암묵적인 규칙이 있다**

코드의 레이아웃을 줄 때 Tap이나 4개의 Space을 사용한다
Python의 문서에서는 4개의 Space를 권하고 있다

클래스 이름은 Camel Case로 작성하고 변수,함수 이름은 Snake Case로 작성한다

👇 예시

```python
class ThisIsExample:

def this_is_example:

```

### Function

---

![](https://images.velog.io/images/action2thefuture/post/d6001851-10e2-41fb-9208-2057fce1e92b/%ED%95%A8%EC%88%98.png)

입력 값을 함수에 넣어서 함수에 의해 결과 값을 얻을 수 있다

#### **Function 정의**

```python
def function():
	return
```

return은 함수로부터 값을 돌려줍니다
return에 어떠한 표현식이 없으면 None을 돌려줍니다

**가변 매개변수 / 키워드 매개변수**

```python
*args 가변 매개변수 **kwargs 키워드 매개변수

def function(*args):
  return args
def function(**kwargs):
  return kwargs
```

가변 매개변수는 `*` / 키워드 매개변수는 `**` 을 사용하여 unpacking을 한다
키워드 매개변수 dictionary 형태로 만들어진다
가변 매개변수는 함수당 하나만 사용가능하고 가변 매개변수 뒤에 일반 매개변수가 올 수 없다
가변 매개변수는 순서에 맞게 할당이 되지만 키워드 매개변수를 이용해 직접 매개변수를 지정하여 불러올 수 있다

### Class

---

**왜 Class를 사용하는가❔**

반복적인 코드 작성과 오류를 감소시킬 수 있고 유지보수를 원활하게 도와준다

**Class 정의**

```
class ClassName:
```

**1. 생성자(Constructor), 메소드(method)**

```python
class ClassName:
  def __init__(self, name, action):
    self.name = name
    self.action = action
  def method(self):
    print("method")
```

Class 안에 만들어진 함수를 method라 부른다
일반적인 함수와 달리 method는 매개변수가 필요하다

> dir() 내장 함수를 이용하여 해당 객체의 method를 확인해볼 수 있다

**2. 인스턴스(Instance)** : Class로 정의된 객체를 변수로 만들어준다

```python
a = ClassName("name", "action")

위 Class에서 self를 제외한 매개변수가 2개이므로 매개변수를 2개 넣어준다
```

Class 이름뒤에 ()를 붙힌다

👇 method 불러오기

```python
a.method()
```

`def method(self)`의 수행문인 `print(method)`이 출력이 된다

**상속(Inheritance)** : 먼저 쓰여진 class를 가져와서 파생 class를 만들어 준다

```python
기반 클래스
class ClassName:
  def __init__(self, name, action):
    self.name = name
    self.action = action
  def method(self):
    print(self.name)

파생 클래스
class Inheritance(ClassName):
  def __init__(self, name, action, shape):
    self.name = name
    self.action = action
    self.shape = shape

인스턴스
a = Inheritance("name", "action", "shape")

method 호출
a.method()
```

`def method(self)`의 수행문인 `print(self.name)`이 출력이 된다

필요에 따라 다중 상속도 가능하다

**3. 반복자(iterator)**

- 값을 하나씩 차례대로 꺼낼 수 있는 객체이다
- 반복 가능한 객체를 확인하는 방법은 dir()을 통해서 `__iter__`가 들어있는지로 판단할 수 있다
  (`문자열`, `리스트`, `딕셔너리`, `세트` 등이 반복가능한 객체이다)
- 이터레이터에서 `__next__`를 호출하면 차례로 하나씩 꺼낼 수 있다
  남은 요소가 없으면, `__next__` 는 StopIteration 예외를 일으킨다

👇이터레이터 작성 예시
![](https://images.velog.io/images/action2thefuture/post/74ea57b6-5f37-4267-be4b-e4f5b5b3c1a3/%EC%98%88%EC%8B%9C5.png)

**❔설명**
마지막 숫자를 5로 지정한 후 `__next__`를 이용하여 하나씩 꺼내고 5를 넘어가면 StopIteration 예외를 일으킨다

**4. 발생자(Generator)**

- 이터레이터를 만들어주는 함수이다
- 일반적인 함수처럼 작성되지만 값을 돌려주고 싶을 때마다 함수 안에서yield을 사용한다
- 이터레이터에서 사용한 `__iter__`와 `__next__` method가 자동적으로 만들어주어서 편리하게 이터레이터를 만들 수 있다

### Generator

👇**제너레이터 작성 예시**

![](https://images.velog.io/images/action2thefuture/post/be696792-20fe-4f67-89b0-7ea0ed4236e0/%EC%98%88%EC%8B%9C%206.png)
👍`__iter__`와 `__next__`를 지정하지 않아도 함수 yield만으로 간단히 작성이 가능하다

---

👇yield from을 이용하면 여러번 yield를 작성하지 않아도 된다

![](https://images.velog.io/images/action2thefuture/post/d8f29c01-ea23-41a7-9713-dfa1295259bc/%EC%98%88%EC%8B%9C%207.png)

---

**👇이터레이터와 제너레이터 패턴구조**

![](https://images.velog.io/images/action2thefuture/post/3b688d6c-b887-4b7f-b02b-acc19bcb4fed/%EC%9D%B4%ED%84%B0%EB%A0%88%EC%9D%B4%ED%84%B0.png)

#### lazy evaluation

time 패키지를 이용하여 지연시간을 발생시키고
random 패키지를 이용하여 난수를 만들었다

```python
import time, random

def random_list(size):

  result = []
  num = 0
  for i in range(size):
    num += random.randint(0,100)
    result.append(num)
  return result

# random.randint()를 이용하여 0부터 100까지의 무작위의 숫자를 불러온다
# random_list(size)는 인자로 size값을 받아 요소 갯수가 size값인 리스트를 만든다

def print_iter(iter):
  for element in iter:
    print(element)

def lazy_return(num):
  sec = 1
  print(f"sleep {sec}s")
  time.sleep(sec)
  return num

#sec값에 따라 지연시간을 변화시킬 수 있다

print("comprehension_list=")

def comprehension_list():
  a = random_list(3)
  comprehension_list = [ lazy_return(i) for i in a ]
  print(comprehension_list)
  return comprehension_list

print_iter(comprehension_list())

# 리스트 표현식을 이용하여 리스트를 만들고 그 리스트를 출력을 하면서
# 각 리스트의 요소들도 출력시킨다

print("generator_exp=")

def generator_exp():
  a = random_list(3)
  gen = ( lazy_return(i) for i in a )
  print(gen)
  return gen
print_iter(generator_exp())

# generator 표현식을 이용하여 generator를 만들어 하나씩 계산값을 출력시킨다
```

👇 **출력값**

![](https://images.velog.io/images/action2thefuture/post/8ee4041b-5ea5-4430-a618-900503dbef04/generator.png)

**lazy evaluation을 이용하는 이유❓**

위 예시로 설명한다면 리스트를 이용한 출력값은 모든 계산값을 메모리에 저장한다음 리스트에 해당 되는 요소들을 그대로 출력한 것이다
하지만 제너레이터를 이용한 출력값은 하나씩 계산을 하면서 출력한 값이므로 메모리를 더욱 적게 쓸것이고 위 예시에서는 구현되진 않았지만 계산에 사용되지 않는 값을 제외하여 쓸데없는 메모리 낭비을 줄일 수 있다
