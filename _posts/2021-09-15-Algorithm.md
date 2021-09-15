---
layout: post
title: "Longest Substring Without Repeating Characters"
date: 2021-09-15
categories: TIL Python 코딩테스트 DynamicProgramming 동적계획법
---

# [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if len(s) == 1:
            return 1

        str_list = []
        for i in range(len(s)-1):
            for j in range(1,len(s)+1):
                if s[i:j] not in str_list:
                    answer = ""
                    for k in s[i:j]:
                        if k not in answer:
                            answer += k
                    if answer in s:
                        str_list.append(len(answer))

        if not str_list:
            return 0
        return max(str_list)
```

슬라이싱을 통한 브루트포스로 풀었지만 시간초과로 탈락

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        used = {} # 문자들의 가장 마지막 위치의 인덱스를 담은 딕셔너리
        max_length = 0 # 나온 길이 중 최대 길이
        start = 0 # 부분 문자열의 첫 문자의 index(초기값:0)
        for i, c in enumerate(s):
            if c in used and start <= used[c]: # 해당 문자열에 dict에 속해있고 and dict에 속해있는 해당 문자열의 위치 인덱스가 시작 인덱스보다 작거나 같다면
                start = used[c] + 1 # 시작 인덱스 변경
            else:
                max_length = max(max_length, i - start + 1)
            used[c] = i # dict 해당 문자열 마지막 위치 인덱스 갱신

        return max_length
```

입력값

```
"abcabcbb"
```

|           used           | max_length | start | str |
| :----------------------: | :--------: | :---: | :-: |
|            {}            |     1      |   0   |     |
|         {'a': 0}         |     2      |   0   |  a  |
|     {'a': 0, 'b': 1}     |     3      |   0   | ab  |
| {'a': 0, 'b': 1, 'c': 2} |     3      |   1   | abc |
| {'a': 3, 'b': 1, 'c': 2} |     3      |   2   |  a  |
| {'a': 3, 'b': 4, 'c': 2} |     3      |   3   | ab  |
| {'a': 3, 'b': 4, 'c': 5} |     3      |   5   | abc |
| {'a': 3, 'b': 6, 'c': 5} |     3      |   7   |  b  |
| {'a': 3, 'b': 6, 'c': 5} |     3      |   7   |  b  |

출력값

```
3
```
