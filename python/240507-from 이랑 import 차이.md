## python from 이랑 import 차이

- `모듈을 불러와서 사용할 때` 입력하는 import와 from의 의미/차이에 대해

## 목차

1. [결론: from과 import의 차이는?](#결론-from과-import의-차이는)
1. [from 모듈명 import 함수](#from-모듈명-import-함수)
1. [사용 예시](#사용-예시)
    - [import os](#import-os)
    - [from os import *](#from-os-import-)
    - [from os import listdir](#from-os-import-listdir)
1. [References](#references)

## 결론: from과 import의 차이는?

- `from`으로 모듈(.py)을 호출해서 사용할 때는 `함수명()`으로 사용
- `import`로 모듈(.py)을 호출해서 사용할 때는 `모듈명.함수명()`응로 사용

## from 모듈명 import 함수

- 보통 `모듈 안의 특정함수만 사용하고 싶을 때` 많이 활용
- from 모듈명 import 함수

어떤 모듈로부터 특정 함수만 내 프로그램으로 포함시킨다.

## 사용 예시

os 모듈의 listdir 함수를 사용하는 상황을 예로 설명
 
- `모듈`: os (운영체제에서 제공되는 여러 기능을 다룰 수 있는 파이썬 모듈)
- `모듈 내의 함수`: listdir (현재 경로의 파일 또는 폴더의 리스트를 반환하는 함수)

### import os

```python
import os
```

- os 모듈을 불러오는 것
- 현재 python 파일에서 listdir 함수를 사용 하려면 `os.listdir()`이라고 입력해야함.

### from os import *

```python
from os import *
```

- 현재 python 파일에서 listdir 함수를 사용하려면 `listdir()`만 사용하면 됨.
- 이때 주의할 점은 from으로 불러온 모듈에 `같은 이름의 함수가 있으면` 문제가 발생.
- 참고로, import *를 와일드 임포트(wild import)라고 부름.

### from os import listdir

- 하나의 함수만 가져오는 것도 가능. (함수 사용법은 case2와 같음)
- 와일드 임포트는 뜻하지 않게 기존의 변수나 함수를 덮어 쓸 때가 있을 수 있으므로 해당 방법이 바람직함.



## References

- [](https://coding-kindergarten.tistory.com/73)
- [](https://kevinitcoding.tistory.com/entry/%EA%B8%B0%EC%B4%88-%ED%8C%8C%EC%9D%B4%EC%8D%ACPython-from%EA%B3%BC-import%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%97%90-%EB%8C%80%ED%95%B4-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90)
