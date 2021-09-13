---
layout: post
title: "deque, list"
date: 2021-09-12
categories: TIL Python 시간복잡도 deque list Tip
---

# [자주 틀리는 요인](https://www.acmicpc.net/blog/view/70)

알고리즘을 풀면서 시간복잡도에 대해 많이 생각하게 된다

정렬이나 queue를 이용하는 문제를 풀 떄 deque를 사용하게 된다

이걸 알기 전까지 나의 생각은 list나 deque의 용도 비슷해서 둘 중에 선택해서 사용을 했다  
list와 deque는 시간복잡도면에서 큰 차이점이 있다는 것을 몰랐다  
list는 인덱스를 가지고 있으므로 pop이나 append같이 추가나 삭제하는 수정사항이 있으면 list의 메모리를 재할당하여 연산속도가 느려진다  
하지만 deque는 인덱스를 가지고 있지 않고 맨 앞이나 뒤로 추가, 삭제만 가능하다  
물론 remove()를 사용해 요소값을 삭제하는 것도 있지만 stack이나 queue 알고리즘에서는 사용되지 않을 것이다  
그러므로 stack이나 queue 문제에서는 list보다 deque를 사용하는 것이 시간복잡도면에서 월등히 좋다

## deque()

- `deque.append(item)`: item을 오른쪽 끝에 삽입한다
- `deque.appendleft(item)`: item을 왼쪽 끝에 삽입한다
- `deque.pop()`: 오른쪽 끝 엘리먼트를 가져오는 동시에 데크에서 삭제한다
- `deque.popleft()`: 왼쪽 끝 엘리먼트를 가져오는 동시에 데크에서 삭제한다
- `deque.extend(array)`: 주어진 배열(array)을 순환하면서 데크의 오른쪽에 추가한다
- `deque.extendleft(array)`: 주어진 배열(array)을 순환하면서 데크의 왼쪽에 추가한다
- `deque.remove(item)`: item을 데크에서 찾아 삭제한다
- `deque.rotate(num)`: 데크를 num만큼 회전한다(양수면 오른쪽, 음수면 왼쪽)

[출처](https://leonkong.cc/posts/python-deque.html)
