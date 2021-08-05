---
layout: post
title: "Hash"
date: 2021-03-24
categories: TIL algorithm hash python 자료구조 DataStructure
---

## Hash

임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수

![](<https://images.velog.io/images/action2thefuture/post/bce5919e-689d-4bbe-925b-4df8384b3cfb/hash%20(1).png>)

### Hash 구조

Hash는 단방향성 구조이다

- Hash Table : 키(key)에 대해 데이터(data)를 저장하는 구조
- Key : input data (위 그림에서 Plain Text)
- Value : 저장할 data
- Hash Value : Hash를 구현한 함수
- Hash : input data가 들어가 고정 길이로 변환된 값

python에서는 dictionay로 hash table을 만들 수 있다

**주요 용도 **

- 보안 및 암호 분야
- 매우 빠른 검색을 위한 소프트웨어 제작
- 데이터 베이스나 테이블 검색
- 캐쉬를 구현하는 경우
- 블록체인

**장점**

- 데이터 저장/ 검색속도가 빠르다
- key에 대한 데이터가 있는지(중복)확인이 쉽다

**단점**

- 많은 저장공간 필요
- 여러 키에 해당하는 주소가 동일할 경우 충돌
- 충돌을 해결하기 위한 자료 구조 필요

### Hash 구현

```python
class HashTable:
  def __init__(self, table_length):
    self.length = table_length
    self.hash_table = list([0 for i in range(self.length)])

  def hashfunction(self, key):
    return key % self.length
  # teble 길이에 따라 key의 길이가 결정된다
  def getkey(self, key):
    self.key = hash(key)
    return self.key
  # hash함수로 key를 부여하는 함수
  # hash()는 python의 내장 함수
  def getAddress(self, key):
    myKey = self.getkey(key)
    hash_address = self.hashfunction(myKey)
    return hash_address
  # hash값을 return 하는 함수
  def insert(self, key, value):
    hash_address = self.getAddress(key)
    self.hash_table[hash_address] = value
  #input값을 hash table에 부여
  def print(self):
    print(self.hash_table)
```

### 충돌 해결 방법

**Hash 충돌** : 해시 함수가 서로 다른 두 개의 입력값에 대해 동일한 출력값을 내는 상황

1.  **Chaining 기법**

- 해쉬 테이블 외의 저장공간을 이용한다
- 충돌이 일어나면 링크드 리스트를 이용해 데이터를 추가로 뒤에 저장을 하여 또 하나의 저장공간을 만든다

2.  **Linear Probing 기법**

- 해쉬 테이블 저장공간 안에서 충돌이 문제를 해결한다
- 충돌이 일어나면 해당 hash addres부터 맨 처음 빈 공간에 저장한다

[해쉬 테이블](https://www.fun-coding.org/Chapter09-hashtable.html)

### Hash 라이브러리

**hashlib을 통해 해쉬 값이 고정된 method를 불러낼 수 있다**

| 해시 알고리즘 | 해쉬 바이트의 크기 | 내부블록의 크기 |
| :-----------: | :----------------: | :-------------: |
|     SHA1      |         20         |       64        |
|    SHA224     |         28         |       64        |
|    SHA256     |         32         |       64        |
|    SHA384     |         48         |       128       |
|    SHA512     |         64         |       128       |

> https://docs.python.org/ko/3.10/library/hashlib.html

```python
import hashlib

string = 'hi'
encoded_string = string.encode()
# 문자열을 바이트로 변환
# 유니코드를 utf-8, ascii 코드 형식의 바이트 코드로 변환
print(encoded_string)
>> b'hi'
hash = hashlib.sha1()
hash.update(encoded_string)
digest = hash.digest()
hexdigest = hash.hexdigest()
hash_size = hash.digest_size
hash_block_size = hash.block_size

print(digest)
>>b'\xc2+_\x91x4&\tB\x8doQ\xb2\xc5\xafL\x0b\xdejB'
print(hexdigest)
>>c22b5f9178342609428d6f51b2c5af4c0bde6a42
print(hash_size)
>>20
print(hash_block_size)
>>64

#만약에 string을 hi.로 변경하면 문자열은 하나가 다르지만 hash값은 완전히 다르다
>> 0d23955fa990b3eb49aad26d9acbe73c83c8202c
```
