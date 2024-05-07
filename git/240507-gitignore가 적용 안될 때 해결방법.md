## 240507-gitignore가 적용 안될 때 해결방법

`.gitignore` 파일에 추가 했는데도 커밋대상에서 제외가 안 되는 경우

- 이럴 때에는 대부분 git 캐시가 문제가 되는 거라 캐시를 삭제해주고 다시 추가해주면 .gitignore 파일이 정상 작동하게된다.

```bash
git rm -r --cached .
git add .
git commit -m "commit 내용"
```

이후 커밋, 푸쉬 해주게 되면 정상 작동한다.


### git rm 옵션

#### -r: recursive removal

- 폴더 안에 다른 파일이 있으면 그 폴더를 지우지 못한다.
- 그래서 폴더를 지우기 전에 안에 있는 내용을 반복적으로 비워주고 지우겠다는 옵션

#### --cached: only remove from the index

- index만 지워준다는 뜻
- index만 지워준다는 뜻은 `Stage Area에서 내려주겠다는 옵션`이다. 이 옵션을 사용하면 git에 있는 인덱스 파일만 삭제하고 `실제 파일은 삭제되지 않음`
  
## References

- [[Git] .gitignore가 적용 안될 때 해결방법](https://velog.io/@kjhxxxx/Git-.gitignore%EA%B0%80-%EC%A0%81%EC%9A%A9-%EC%95%88%EB%90%A0-%EB%95%8C-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)
