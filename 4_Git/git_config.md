# Git 설정 및 GitHub 연동
## 체크 리스트
- [x] Git 사용자 정보 설정 (user.name, user.email)
- [x] 기본 브랜치 이름 설정 (init.defaultBranch)
- [x] Git 설정 전체 목록 확인 (git config --list)


## Git 기본 사용자 및 브랜치 설정
### Git 사용자 정보 설정
- Git 저장소에 커밋 내역을 기록할 때 사용될 사용자 이름과 이메일을 설정합니다.
- GitHub 계정 정보와 동일하게 작성하는 것을 권장합니다.
- `--global` : 현재 시스템의 모든 Git 저장소에 공통으로 적용되는 옵션입니다.

``` bash
git config --global user.name "사용자이름"
git config --global user.email "이메일주소"
```

``` Bash
singainnn6931@c4r2s5 4_Git % git config --global user.name "hena"
singainnn6931@c4r2s5 4_Git % git config --global user.email "hena.journey@google.com"
```
### 기본 브랜치 이름 설정
- git init으로 새 저장소를 생성할 때 만들어질 기본 브랜치 이름을 설정합니다.
- 최신 표준 권장 사항에 맞춰 main으로 지정합니다.

``` bash
git config --global init.defaultBranch main
```

``` bash
singainnn6931@c4r2s5 4_Git % git config --global init.defaultBranch main
```
### Git 전체 설정 목록 확인
- 현재 시스템 및 프로젝트에 설정된 모든 Git 옵션을 출력합니다.
- 설정이 올바르게 되었는지 확인할 때 사용합니다.

```bash
git config --list
```
```bash
singainnn6931@c4r2s5 1_LearnSetting % git config --list                 
credential.helper=osxkeychain
user.name=hena
user.email=hena.journey@gmail.com
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
remote.origin.url=https://github.com/hena-archive/Codyssey_B1_Setting.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
user.name=hena
```

|구분| `--global`| 로컬 설정 (`--local` 또는 생략)|
|--|--|--|
|적용 범위|내 컴퓨터의 모든 Git 프로젝트 전체|현재 위치한 특정 Git 프로젝트 1개|
|설정 위치|사용자 홈 디렉토리 (~/.gitconfig)|프로젝트 내부 폴더 (.git/config)|
|우선순위|낮음 (로컬 설정이 없을 때 적용)|프높음 (글로벌 설정을 덮어씀)|
|주요 용도|내 개인 PC의 기본 이름/이메일 지정|회사용/개인용 프로젝트별 계정 분리|
