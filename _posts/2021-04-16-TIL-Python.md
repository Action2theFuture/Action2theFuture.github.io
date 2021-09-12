---
layout: post
title: "Python | Module"
date: 2021-04-16
categories: TIL Module Import Path Python
---

## sys

### sys.modules / sys.path

import하는 package나 module을 확인하기 위해 사용된다

**순서**

sys.modules >> built-in modules >> sys.path

#### **sys.modules**

제일 처음 처음 경로를 판단하기 위해서 사용된다
새로 import된 Module/Package는 나오지 않는다
딕셔너리 형태로 Modules / Package의 경로

#### Bulit-in Modules

파이썬을 설치할 때 내장된 Library이다(sys, math 등등)

#### **sys.path**

리스트 형태로 Modules / Package의 디렉토리
![](https://images.velog.io/images/action2thefuture/post/1f6c17b2-2e66-4c3f-8732-191d6a6465c2/path.png)

sys.path는 리스트 형태이므로 append()를 이용하여 경로를 추가할 수 있다

sys.path에서도 모듈을 발견하지 못하면 **ModuleNotFoundError 에러**를 리턴

---

## Package

#### Absolute path / relative path

- **Absolute path**

어느 위치에 있던 항상 같은 경로를 나타낸다
프로젝트의 최상단에서 경로를 시작하게 된다

- **relative path**

현재에 위치한 곳에서 해당되는 위치에 대한 경로이다
위치한 곳에 따라 경로가 달라지므로 디렉토리 내의 파일 경로를 사용자가 확인이 필요하다
![](https://images.velog.io/images/action2thefuture/post/a5bcc895-aacd-4491-8cd5-c4e70d1603e3/tree.png)

### 1. Main.py(상대경로 / 절대경로)

**👇 Main.py에서 상대경로로 임포트를 했을 때**

![](https://images.velog.io/images/action2thefuture/post/32217483-2fdf-4a19-91d7-8746770e10ae/relativve%20path.png)

import를 하지 못하고 에러발생

**👇 Main.py에서 절대경로로 임포트를 했을 때**

![](https://images.velog.io/images/action2thefuture/post/eeeef1aa-4618-40f1-a6d3-10ad49ef2ce5/absolute%20path.png)

절대경로로 import를 하니 정상적으로 계산 값이 출력이 되었다

python 공식문서를 참조하면

👉상대 임포트가 현재 모듈의 이름에 기반을 둔다는 것에 주의하세요. 메인 모듈의 이름은 항상 "**main**" 이기 때문에,
파이썬 **응용 프로그램의 메인 모듈로 사용될 목적의 모듈들**은 반드시 **절대 임포트를 사용**해야 합니다.

### 2. 패키지 내부 파일(상대경로 / 절대경로)

![](https://images.velog.io/images/action2thefuture/post/b9a2170a-9a79-46ab-8a9e-6a1e48140503/multiply.png)

### 3. `__init__.py`

#### 1. `__init__.py`

`__init__.py`를 통하여 해당 디렉토리가 패키지라는 것을 알려준다

#### 2. `__all__`

`*`을 이용하여 import할시 `__init__.py`내에 `__all__`라는 변수를 설정하여 import를 할 모듈을 정해주어야 인식이 가능하다

**📣 예시**
![](https://images.velog.io/images/action2thefuture/post/a5bcc895-aacd-4491-8cd5-c4e70d1603e3/tree.png)

**👇 `__init__py`인 파일에 `__all__`에 `add_and_multiply`는 제외하고 `multiplication`만 포함시켜본다**

![](https://images.velog.io/images/action2thefuture/post/43338664-5c9e-4f46-81b8-1b55c187570a/all.png)

**👇 import를 해보니 `add_and_multiply.py`를 인식하지 못 한다**

![](https://images.velog.io/images/action2thefuture/post/116d7af0-8892-4538-9cd5-9455dd1bb997/all2.png)

**👇 다시 `__init__.py`로 돌아가 `__all__`에 `add_and_multiply`도 포함시켜본다**

![](https://images.velog.io/images/action2thefuture/post/0fd1ca21-155f-4289-b32e-df3ae6a49e3b/all3.png)

**👇 에러가 해결되고 정상적으로 출력이 되었다**

![](https://images.velog.io/images/action2thefuture/post/95d71854-30ee-4592-bd8b-c3c5cd83e90a/all4.png)

[파이썬 패키지에 대한 공식문서](https://docs.python.org/ko/3/tutorial/modules.html#intra-package-references)
