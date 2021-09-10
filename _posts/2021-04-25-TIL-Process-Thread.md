---
layout: post
title: "Process Thread"
date: 2021-04-25
categories: TIL Thread process Python
---

![](https://images.velog.io/images/action2thefuture/post/43fbb940-fbf5-44d5-9a83-3eff8351ebec/thread.png)
(이미지 출처 : [링크](<https://en.wikipedia.org/wiki/Thread_(computing)>))

## Process vs Thread

### Process

👉 **현재 실행되고 있는 프로그램**
process의 내부에는 **최소한 1개의 Thread**를 가지고 있다
![](https://images.velog.io/images/action2thefuture/post/7cc6dae5-cd2d-4aa4-baaf-ef46c2a9f384/process%20memory.png)

#### Process 내의 메모리 영역

![](https://images.velog.io/images/action2thefuture/post/7294b8ab-19cb-4c30-8243-149511a320f4/memory%20%EC%98%81%EC%97%AD.png)
(이미지 출처 : [링크](http://www.tcpschool.com/c/c_memory_structure))
**process에는 각 구조의 역할이 있는 메모리 구조를 가지고 있다**

**1. code**
code를 가지고 있는 메모리 영역, 프로그램에 대한 명령어가 들어가 있다

**2. data**
전역변수, 정적변수, 배열, 구조체들이 저장이 되고 프로그램이 종료되면 초기화가 되는 데이터가 저장이 되고 그렇지 않은 데이터는 BSS(Block stated symbol)에 저장이 된다

**3. stack**
동적인 상태가 될 때 사용이 되며 C언어에서 malloc(), calloc()를 사용하여 자율적으로 메모리를 할당할 수 있다
python에서는 자동적으로 Python Memory Manager를 이용하여 메모리의 할당 범위를 조정해준다

**4. heap**
stack과 마찬가지로 프로그램이 동적인 상태가 될 때 사용되는 메모리영역으로 지역변수, 매개변수, 리턴값 등이 저장이 되고 런타임이 끝나면 반환을 한다 heap은 stack과 달리 크기가 고정되어 있다

### Thread

![](https://images.velog.io/images/action2thefuture/post/33ead0b6-0000-4fe7-b34e-7a10dec2d1ec/memory%20process.png)
(이미지 출처 : [링크](https://www.crocus.co.kr/1403))
Thread는 서로 메모리를 공유(Code, Data, Heap)하면서 실행이 된다
Thread는 각자 수행해야할 함수들이 있고 독립적으로 작업을 하므로 **독립적인 stack 메모리 영역**을 갖는다

#### 👇 Thread 동기화

```python
import time

if __name__ == "__main__":

    increased_num = 0

    start_time = time.time()
    for i in range(1000000):
        increased_num += 1

    print("--- %s seconds ---" % (time.time() - start_time))

    print("increased_num=",end=""), print(increased_num)
    print("end of main")
```

1000000까지의 숫자를 세는 함수를 만들고 계산을 마칠 때 걸린 시간을 출력한다

**👀출력**
![](https://images.velog.io/images/action2thefuture/post/665b7139-d07c-4106-8b05-645e88b25d0c/ex%201.png)
**🏃‍♀️Thread 적용🏃‍♂️**

```python
import threading
import time

shared_number = 0

def thread_1(number):
    global shared_number
    print("number = ",end=""), print(number)

    for _ in range(number):
        shared_number += 1

def thread_2(number):
    global shared_number
    print("number = ",end=""), print(number)
    for _ in range(number):
        shared_number += 1


if __name__ == "__main__":

    threads = [ ]

    start_time = time.time()
    t1 = threading.Thread( target= thread_1, args=(1000000,) )
    t1.start()
    threads.append(t1)

    t2 = threading.Thread( target= thread_2, args=(1000000,) )
    t2.start()
    threads.append(t2)


    for t in threads:
        t.join()

    print("--- %s seconds ---" % (time.time() - start_time))

    print("shared_number=",end=""), print(shared_number)
    print("end of main")
```

Thread를 이용하여 똑같이 1000000까지의 숫자를 계산하여 각자의 Thread를 만들었다 그리고 join을 하여서 계산을 마치면 걸린 시간과 각 Thread가 1000000까지의 숫자를 센 값이 전역변수인 shared_number에 나온다
하지만 예상과 다르게 1000000과 다른 계산값이 나오고 걸린 시간이 늘어났다

**각 Thread가 동일하게 같은 숫자를 셌으므로 Thread를 사용한 목적을 잃어버렸다**

**👀출력**

![](https://images.velog.io/images/action2thefuture/post/d329d84e-2710-4a0c-a638-435cebddee88/ex%204.png)

**🔗 Thread join**

![](https://images.velog.io/images/action2thefuture/post/900f0b3b-2c43-4253-aa12-e0694d40e45d/thread%20join.png)

그래서 1000000까지의 숫자를 Thread1은 0~500000, Thread2는 500000~1000000 숫자를 계산하게 만들어보았다

```python
import threading
import time

shared_number = 0
def thread_1(number):
    global shared_number
    print("number = ",end=""), print(number//2)

    for _ in range(number//2):
        shared_number += 1

def thread_2(number):
    global shared_number
    print("number = ",end=""), print(number//2)
    for _ in range(number//2,number):
        shared_number += 1


if __name__ == "__main__":

    threads = [ ]

    start_time = time.time()
    t1 = threading.Thread( target= thread_1, args=(1000000,) )
    t1.start()
    threads.append(t1)

    t2 = threading.Thread( target= thread_2, args=(1000000,) )
    t2.start()
    threads.append(t2)


    for t in threads:
        t.join()

    print("--- %s seconds ---" % (time.time() - start_time))

    print("shared_number=",end=""), print(shared_number)
    print("end of main")
```

**👀출력**

![](https://images.velog.io/images/action2thefuture/post/159b511e-6fce-456d-8804-a83a10573c2e/ex%202.png)

Thread를 사용하지 않은 시간보다 약간 줄어들었지만 shared_number를 보니 여전히 각 Thread가 센 숫자보다 큰 값이 나왔다

**뮤텍스(Lock) 사용**

한 자원에 여러 Thread가 접근하는 것을 방지
예시에 해당하는 자원은 변수이다

```python
import threading
import time

lock = threading.Lock()

shared_number = 0

def thread_1(number):
    lock.acquire()
    global shared_number
    print("number = ",end=""), print(number//2)
    for _ in range(number//2):
        shared_number += 1
    lock.release()

def thread_2(number):
    lock.acquire()
    global shared_number
    print("number = ",end=""), print(number//2)
    for _ in range(number//2,number):
        shared_number += 1
    lock.release()



if __name__ == "__main__":

    threads = [ ]

    start_time = time.time()
    t1 = threading.Thread( target= thread_1, args=(1000000,) )
    t1.start()
    threads.append(t1)

    t2 = threading.Thread( target= thread_2, args=(1000000,) )
    t2.start()
    threads.append(t2)


    for t in threads:
        t.join()

    print("--- %s seconds ---" % (time.time() - start_time))

    print("shared_number=",end=""), print(shared_number)
    print("end of main\n")
```

**👀출력**

![](https://images.velog.io/images/action2thefuture/post/430dc11b-c68d-44ec-a621-5c6476cb8fdb/ex%203.png)

Threading 모듈에서 제공하는 lock을 이용하여 첫번째 Thread의 작업이 종료될 때까지 해당 변수를 사용한 뒤 두번째 Thread가 그 변수를 뒤이어 사용하여 shared_number의 값이 기대값인 1000000으로 정확히 나오게 되었다

## Feedback

병렬구조 Thread를 만들어서 효율성을 올리려는 목적이었지만 병렬구조 Thread가 아닌 동기적인 작업이 되어서 목적에는 달성하지 못하였다 하지만 Thread이 왜 사용되는지 어떻게 사용되는지에 대한 정보를 알게되었다
