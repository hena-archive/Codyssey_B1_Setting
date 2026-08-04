# Git 설정 및 GitHub 연동


## 체크 리스트
- [x] Git 사용자 정보 설정 (`user.name`, `user.email`)
- [x] 기본 브랜치 설정 (`init.defaultBranch`)
- [x] Git 설정 확인 (`git config --list`)
- [x] GitHub 원격 저장소 연동 확인
- [x] VS Code GitHub 로그인 확인
- [x] 궁금증 해결하기
  - [x] `--system` vs `--global` vs `--local` 옵션


## Git 기본 설정


### Git 사용자 정보 설정
- Git 저장소에 커밋 내역을 기록할 때 사용될 사용자 이름과 이메일을 설정합니다.
- 커밋 작성자의 정보로 기록되므로, 일반적으로 GitHub 계정과 동일한 이름과 이메일을 사용하는 것을 권장합니다.
- `--global` : 현재 시스템의 모든 Git 저장소에 공통으로 적용되는 옵션입니다.

```bash
git config [옵션] user.name "사용자 이름"
git config [옵션] user.email "이메일 주소"
```


### 구성 요소
| 항목 | 설명 |
|------|------|
| `git config` | Git 설정을 조회하거나 변경하는 명령어입니다. |
| `[옵션]` | 설정 범위를 지정합니다. 일반적으로 `--global` 또는 `--local`을 사용합니다. |
| `user.name` | 커밋 작성자의 이름을 설정합니다. |
| `user.email` | 커밋 작성자의 이메일 주소를 설정합니다. |
| `"사용자 이름"` | 커밋 기록에 표시될 사용자 이름입니다. |
| `"이메일 주소"` | 커밋 기록에 표시될 이메일 주소입니다. |

| 옵션 | 설명 |
|------|------|
| `--global` | 현재 사용자 계정의 모든 Git 저장소에 적용합니다. |
| `--local` | 현재 Git 저장소에만 적용합니다. (기본값) |
| `--system` | 시스템 전체에 적용합니다. (관리자 권한 필요) |

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 4_Git % git config --global user.name "hena"
singainnn6931@c4r2s5 4_Git % git config --global user.email "hena.journey@gmail.com"
```

</details>


### 기본 브랜치 이름 설정
- 새로운 Git 저장소를 생성할 때 기본 브랜치 이름을 `main`으로 설정합니다.
- 이후 `git init`으로 생성되는 새로운 저장소는 기본 브랜치가 `main`으로 생성됩니다.


### 명령어 형식
```bash
git config [옵션] init.defaultBranch [브랜치 이름]
```


### 구성 요소
| 항목 | 설명 |
|------|------|
| `git config` | Git 설정을 조회하거나 변경하는 명령어입니다. |
| `[옵션]` | 설정 범위를 지정하는 옵션입니다. (`--global`, `--local` 등) |
| `init.defaultBranch` | 새 Git 저장소를 생성할 때 사용할 기본 브랜치 이름을 설정하는 항목입니다. |
| `[브랜치 이름]` | 기본 브랜치로 사용할 이름입니다. 일반적으로 `main`을 사용합니다. |


<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 4_Git % git config --global init.defaultBranch main
```

</details>


## Git 전체 설정 목록 확인
- 현재 시스템 및 프로젝트에 설정된 모든 Git 옵션을 출력합니다.
- 설정이 올바르게 되었는지 확인할 때 사용합니다.

```bash
git config [옵션] --list
```

### 구성 요소

| 항목 | 설명 |
|------|------|
| `git config` | Git 설정을 조회하거나 변경하는 명령어입니다. |
| `[옵션]` | 설정 범위를 지정하는 옵션입니다. (`--global`, `--local` 등) |
| `--list` | 현재 적용된 Git 설정 목록을 출력합니다. |

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Setting % git config --list
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
branch.main.vscode-merge-base=origin/main
```

</details>


## GitHub 저장소 연동


### GitHub 원격 저장소 확인
- 현재 Git 저장소에 등록된 원격(Remote) 저장소를 관리하거나 조회하는 명령어입니다.
```bash
git remote [-v]
```

### 구성 요소
| 항목 | 설명 |
|------|------|
| `git remote` | 현재 Git 저장소에 등록된 원격(Remote) 저장소를 관리하거나 조회하는 명령어입니다. |
| `-v` | 원격 저장소의 이름과 Fetch/Push URL을 함께 출력합니다. |

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Setting % git remote -v
origin  https://github.com/hena-archive/Codyssey_B1_Setting.git (fetch)
origin  https://github.com/hena-archive/Codyssey_B1_Setting.git (push)
```
실행 결과에서 `origin`의 Fetch와 Push URL이 모두 출력되므로,
현재 Git 저장소가 GitHub 원격 저장소와 정상적으로 연결되어 있음을 확인할 수 있습니다.


</details>


### VS Code GitHub 로그인 확인
VS Code 왼쪽 아래의 **계정(Accounts)** 아이콘을 클릭하면 현재 로그인한 GitHub 계정을 확인할 수 있습니다.
로그인되어 있다면 **Signed in to GitHub**가 표시되며,
로그인되어 있지 않은 경우에는 **Sign in to GitHub**가 표시됩니다.

<details>
<summary>VS Code 화면</summary>

로그인되어 있지 않다면 Sign in to GitHub가 표시됩니다.
![VS code와 Github연동](<VSCodeAndGithub.png>)

</details>

## 궁금한거 찾아보기


### `--system` vs `--global` vs `--local` 옵션 비교하기
| 구분 | `--system` | `--global` | `--local` (또는 옵션 생략) |
|------|------------|------------|-----------------------------|
| 적용 범위 | 컴퓨터의 모든 사용자와 모든 Git 저장소 | 현재 사용자의 모든 Git 저장소 | 현재 Git 저장소만 |
| 설정 위치 | 시스템 Git 설정 파일 (예: `/etc/gitconfig`) | `~/.gitconfig` | `.git/config` |
| 우선순위 | 가장 낮음 | 중간 | 가장 높음 (`System`, `Global` 설정을 덮어씀) |
| 주요 용도 | 시스템 관리자(OS 관리자)가 공통 설정 | 개인 기본 설정(이름, 이메일 등) | 프로젝트별 설정(회사/개인 계정 분리 등) |
| 권한 | 관리자(root) 권한 필요 | 일반 사용자 가능 | 일반 사용자 가능 |
