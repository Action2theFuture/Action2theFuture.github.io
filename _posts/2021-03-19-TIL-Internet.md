---
layout: post
title: "Internet"
date: 2021-03-19
categories: TIL DNS Browser Network Internet
---

## 인터넷(Internet)

---

통신 프로토콜을 이용해 정보를 주고받는 컴퓨터 네트워크

### 어떻게 작동하는가❓

각 Host들은 네트워크 안에서 서로 간의 규약으로 데이터를 공유한다

### 네트워크 계층

---

#### OSI 7계층

![](https://images.velog.io/images/action2thefuture/post/dc76a0c5-aac1-4133-b550-ce41e6b483ef/OSI%207%20layer.jpg)
OSI(Open System Interconnection)
상호연결에 대한 절차를 7단계로 나눈 시스템

**1. 물리계층(Physical Layer)**

- 데이터 전송 유무
- 아날로그 신호를 디지털 신호로 전환
- 광케이블, 리피터, 허브, PHY칩

**2. 데이터링크계층(DataLink Layer)**

- 안전한 정보(프레임) 전달(에러검출/재전송/흐름제어)
- 3계층에서 정보를 받아 주소와 에러 정보를 헤더와 테일에 추가
- MAC(Media Access Control) 주소로 통신
  예시 ➡ `00:1A:2B:3C:4D:5E`의 형식
- 스위치, 브리지

**3. 네트워크계층(Network Layer)**

- IP 주소 관리/라우팅(어떤 네트워크 안에서 통신 데이터를 보낼 때 최적의 경로를 선택하는 과정)
- IP주소를 이용한 후(`Routing`) 다음 라우터에게 전달한다(`Forwarding`)

**라우팅 테이블을 이용하여 경로를 찾는다**
![](https://images.velog.io/images/action2thefuture/post/695443e0-c233-41c9-9097-67c48e190ec9/%EB%9D%BC%EC%9A%B0%ED%8C%85%20%ED%85%8C%EC%9D%B4%EB%B8%94.png)

**4. 전송계층**

- Packet 생성 및 오류 관리, 오류시 재송신
  `Port Number`를 부여
  (하나의 컴퓨터에서 특정 프로세스를 식별하기 위한 논리값)
- TCP 프로토콜 **신뢰성 보장**/연결지향적
- UDP 프로토콜 **신뢰성 낮음**/실시간 응용, 멀티태스킹 가능/헤더가 단순

**5. 세션계층**

- 데이터가 통신하기 위한 연결 유지
- 동시송수신방식(duplex), 반이중방식(half-duplex), 전이중방식(Full duplex)
- `TCP/IP` 세션을 만들고 없앤다

**6. 표현계층**

- 공통된 표준 형식을 이용
- 데이터 포맷 , 암호화
- 인코딩/암호화

**7. 응용계층**

- `HTTP`, `FTP`, `SMTP`, `POP3`, `IMAP`, `Telnet`
- 응용서비스 수행

**Encapsulation & Decapsulation**
![](https://images.velog.io/images/action2thefuture/post/04a86e8c-9c3b-4602-98a7-3e3945795f25/packet.gif)
**사용자의 데이터는 각 계층의 header로 Encapsulation이 된다**
송신자 `Encapsulation`
수신자 `Decapsulation`

#### TCP/IP Protocol & TCP/IP Protocol updated

---

현재 OSI 7계층보다 TCP/IP Protocol이 많이 쓰인다
![](https://images.velog.io/images/action2thefuture/post/5b6bd7b9-50af-4831-816e-3cec6e9aef3a/osi_1.jpg)

---

**HTTP**
![](https://images.velog.io/images/action2thefuture/post/154f5f8a-abff-481d-929e-3d160691b4d1/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8%20&%20%EC%84%9C%EB%B2%84.jpg)

1. 요청 및 응답 구조

   1. Method

   - GET
     데이터를 받아올 때
   - POST
     데이터를 생성/수정 할 떄 사용
   - DELETE
     서버에 저장된 특정 데이터 삭제

   2. Header
      요청과 응답에 대한 추가 정보 (메타 데이터)

   3. body
      요청과 응답의 실제 정보

**상태 코드**

    |상태 코드|정의|
    |-----|--------|
    |200|OK|
    |201|Created|
    |400|bad request|
    |401|unauthoirized|
    |403|forbidden|
    |404|not found|
    |405|method not allowed|
    |500|internal server error|

2. 메세지 교환 형태의 프로토콜
   - 클라이언트와 서버 간에 `HTTP 메세지`를 주고받으며 통신
     SMTP 전자메일 프로토콜과 유사
   - `HTTP`의 응답 및 요청 메세지 구성
   - `HTTP 메세지` 내 헤더 항목들
3. 트랙잭션 중심의 비연결성 프로토콜
   - 종단간 연결이 없음 (Connectionless)
   - 이전의 상태를 유지하지 않음 (Stateless)
4. 전송계층 프로토콜 및 사용 포트번호
   - 전송계층 프로토콜 : `TCP`
   - 사용 포트 번호 : 80번

---

> https://shlee0882.tistory.com/110 >https://brownbears.tistory.com/189
