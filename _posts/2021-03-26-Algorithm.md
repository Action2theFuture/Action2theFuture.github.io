---
layout: post
title: "문자열압축"
date: 2021-03-26
categories: TIL Level2 algorithm programmers 코딩테스트
---

# [문자열압축](https://programmers.co.kr/learn/courses/30/lessons/60057)

**문제 설명**

데이터 처리 전문가가 되고 싶은 "어피치"는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, "ababcdcdababcdcd"의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 "2ab2cd2ab2cd"로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 "2ababcdcd"로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, "abcabcdede"와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 "abcabc2de"가 되지만, 3개 단위로 자른다면 "2abcdede"가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

**제한사항**

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.

**입출력 예**

| s                          | result |
| -------------------------- | ------ |
| "aabbaccc"                 | 7      |
| "ababcdcdababcdcd"         | 9      |
| "abcabcdede"               | 8      |
| "abcabcabcabcdededededede" | 14     |
| "xababcdcdababcdcd"        | 17     |

**입출력 예에 대한 설명**
입출력 예 #1

문자열을 1개 단위로 잘라 압축했을 때 가장 짧습니다.

입출력 예 #2

문자열을 8개 단위로 잘라 압축했을 때 가장 짧습니다.

입출력 예 #3

문자열을 3개 단위로 잘라 압축했을 때 가장 짧습니다.

입출력 예 #4

문자열을 2개 단위로 자르면 "abcabcabcabc6de" 가 됩니다.
문자열을 3개 단위로 자르면 "4abcdededededede" 가 됩니다.
문자열을 4개 단위로 자르면 "abcabcabcabc3dede" 가 됩니다.
문자열을 6개 단위로 자를 경우 "2abcabc2dedede"가 되며, 이때의 길이가 14로 가장 짧습니다.

입출력 예 #5

문자열은 제일 앞부터 정해진 길이만큼 잘라야 합니다.
따라서 주어진 문자열을 x / ababcdcd / ababcdcd 로 자르는 것은 불가능 합니다.
이 경우 어떻게 문자열을 잘라도 압축되지 않으므로 가장 짧은 길이는 17이 됩니다.

**문제 풀이**

**첫번째 풀이**

```python
def solution(s):
    w = ""
    count = 1
    answer = ""
    for i in s:
        if w == i:
            count += 1
        else:
            if w != "":
                if count == 1:
                    answer += w
                else:
                    answer += str(count)+w
            w = i
            count = 1
    if count == 1:
        answer += w
    else:
        answer += str(count)+w
    return len(answer)
#먼저 한글자 단위로 끊는 알고리즘 구현
```

**두번째 풀이**

```python
def solution(s):
    if len(s) == 1:
        return 1
    answer = []
    w = ""
    for i in range(1, len(s)):
        count = 1
        word = s[:i] #문자열 길이 나누기
        for j in range(i, len(s), i):
        #i부터 시작해서 i만큼의 스텝으로 범위를 만든다
            if s[j:j+i] == word: #잘린 문자열과 다음 문자열이 같다면
                count += 1
            else:
                if count == 1: #잘린 문자열의 count 리셋
                    count = ""
                w += str(count)+word #해당 문자열을 w에 보관
                word = s[j:j+i] #다음 문자열 시작
                count = 1

        if count == 1: #마지막 반복되는 문자열에대한 생략때문에 위의 조건문과 동일하게 추가
            count = ""
        w += str(count)+word

        answer.append(len(w))
        w = "" #단위 문자열의 재시작위해 초기화
    return min(answer)
```

**다른 사람 풀이**

```python
def compress(text, tok_len):
    words = [text[i:i+tok_len] for i in range(0, len(text), tok_len)]
    res = []
    cur_word = words[0]
    cur_cnt = 1
    for a, b in zip(words, words[1:] + ['']):
        if a == b:
            cur_cnt += 1
        else:
            res.append([cur_word, cur_cnt])
            cur_word = b
            cur_cnt = 1
    return sum(len(word) + (len(str(cnt)) if cnt > 1 else 0) for word, cnt in res)

def solution(text):
    return min(compress(text, tok_len) for tok_len in list(range(1, int(len(text)/2) + 1)) + [len(text)])
```
