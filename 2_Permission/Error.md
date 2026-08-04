# 문제 상황

```bash
singainnn6931@c4r2s5 2_Permission % chmod -R 000 default_directory
chmod: default_directory: Permission denied
```

# 원인
`default_directory`의 권한이 `000(d---------)`으로 바뀐 상태였다. `chmod -R`은 하위 디렉터리와 파일의 권한을 변경하기 위해 디렉터리를 탐색해야 하지만, 실행(`x`) 권한이 없어 디렉터리에 접근하지 못해 `Permission denied` 오류가 발생하였다.

# 해결
디렉터리 자체의 권한을 부여하였다.