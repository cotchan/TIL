## 이분탐색에서 upperbound,lowerbound 구하는 법

문제링크: [숫자 카드 2](https://www.acmicpc.net/problem/10816)

- UpperBound, LowerBound 모두 `기본 탐색 코드는 동일`하다.
- 다른 점은, `target == candidate 케이스`만 별도로 분리해서 max(result, mid), min(result, mid)를 구해야함
  - UpperBound: `maxValue` 구해야함
  - LowerBound: `minValue` 구해야함
- 리스트 내의 숫자 개수는 `upper - lower + 1`

## UpperBound, LowerBound 구하는 코드(이분 탐색)

```python
def getUpperBound(numbers, target, st, en):
    result = -sys.maxsize - 1

    while st < en:
        mid = (st + en) // 2
        candidate = numbers[mid]

        if candidate > target:
            en = mid
        elif candidate < target:
            st = mid + 1
        else:  # candidate == target
            result = max(result, mid)
            st = mid + 1

    return result


def getLowerBound(numbers, target, st, en):
    result = sys.maxsize

    while st < en:
        mid = (st + en) // 2
        candidate = numbers[mid]

        if candidate > target:
            en = mid
        elif candidate < target:
            st = mid + 1
        else:  # candidate == target
            result = min(result, mid)
            en = mid

    return result
```

## 정답코드

```python
from os import sys

N = int(input())
numbers = list(map(int, input().split()))

M = int(input())
targets = list(map(int, input().split()))

numbers.sort()


def getLowerBound(numbers, target, st, en):
    result = sys.maxsize

    while st < en:
        mid = (st + en) // 2
        candidate = numbers[mid]

        if candidate >= target:
            if candidate == target:
                result = min(result, mid)
            en = mid
        elif candidate < target:
            st = mid + 1

    return result


def getUpperBound(numbers, target, st, en):
    result = -sys.maxsize - 1

    while st < en:
        mid = (st + en) // 2
        candidate = numbers[mid]

        if candidate > target:
            en = mid
        elif candidate <= target:
            if candidate == target:
                result = max(result, mid)
            st = mid + 1

    return result


answers = []
numberSize = len(numbers)
for target in targets:
    lower = getLowerBound(numbers, target, 0, numberSize)
    upper = getUpperBound(numbers, target, 0, numberSize)

    if lower == sys.maxsize or upper == -sys.maxsize - 1:
        answers.append(0)
    else:
        answers.append(upper - lower + 1)

print(" ".join(list(map(str, answers))))
```
