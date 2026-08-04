# 권한 기초 실습


### 권한 체크 리스트
- [x] 권한(Permission)

- [x] `chmod`
  - [x] 숫자 표기법
  - [x] 문자 표기법
  - [x] `-R` 옵션
 
- [x] `umask`

- [x] `chown`

- [x] `chgrp`

- [x] `id`

- [x] `stat`

### 초기 세팅
``` bash
# 빈 파일 생성
singainnn6931@c4r2s5 2_Permission % touch default_file

# 빈 디렉토리 생성
singainnn6931@c4r2s5 2_Permission % mkdir default_directory

# 확인
singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  135 Jul 30 14:06 Permission_Command.md
drwxr-xr-x  2 singainnn6931  singainnn6931   64 Jul 30 14:09 default_directory
-rw-r--r--  1 singainnn6931  singainnn6931    0 Jul 30 14:09 default_file
```

## 권한 (Permission)

권한(Permission)은 **사용자가 파일이나 디렉터리에 대해 읽기(Read), 쓰기(Write), 실행(Execute) 작업을 수행할 수 있는 범위를 의미한다.**

### 권한의 대상

- **소유자(Owner)** : 파일 또는 디렉터리의 소유자이다. 기본적으로 생성한 사용자가 소유자가 되며, `chown` 명령어를 통해 변경할 수 있다.
- **그룹(Group)** : 파일 또는 디렉터리에 지정된 그룹에 속한 사용자이다.
- **기타 사용자(Other)** : 소유자와 그룹을 제외한 모든 사용자이다.
- **최고 관리자(Root)** : 시스템의 모든 파일과 디렉터리에 대한 권한을 가지며, 소유자와 관계없이 접근 및 권한 변경이 가능하다.


```text
-   rwx   rwx   rwx
│    │     │     │
│    │     │     └── 기타 사용자(Other)
│    │     └──────── 그룹(Group)
│    └────────────── 소유자(Owner)
└─────────────────── 파일 종류
```

### 파일 종류

`ls -l` 명령어의 첫 번째 문자는 파일의 종류를 나타낸다.

| 문자 | 의미 |
| :--: | :--- |
| `-` | 일반 파일 (Regular File) |
| `d` | 디렉터리 (Directory) |
| `l` | 심볼릭 링크 (Symbolic Link) |

### 권한 종류

권한은 읽기(Read), 쓰기(Write), 실행(Execute) 권한으로 구성된다.

| 문자 | 의미 |
| :--: | :--- |
| `r` | 읽기(Read) 권한 |
| `w` | 쓰기(Write) 권한 |
| `x` | 실행(Execute) 권한 |
| `-` | 해당 권한 없음 |


## `chmod` 숫자 표기법
- 숫자(8진수)를 사용하여 파일이나 디렉터리의 권한을 변경하는 방식
```bash
chmod [권한(3자리 숫자)] [파일 또는 디렉터리]
```

| 자리 | 대상 |
| :---: | :--- |
| 첫 번째 | 소유자(Owner) |
| 두 번째 | 그룹(Group) |
| 세 번째 | 기타 사용자(Other) |

### 숫자 권한 계산

| 권한 | 값 |
|------|---:|
| r (Read) | 4 |
| w (Write) | 2 |
| x (Execute) | 1 |

권한 값은 각 권한의 값을 더하여 계산한다.

| 숫자 | 권한 | 계산 |
|------|------|------|
| 7 | rwx | 4 + 2 + 1 |
| 6 | rw- | 4 + 2 |
| 5 | r-x | 4 + 1 |
| 4 | r-- | 4 |
| 3 | -wx | 2 + 1 |
| 2 | -w- | 2 |
| 1 | --x | 1 |
| 0 | --- | 0 |

<details>
<summary>실행 결과</summary>

### 파일 권한 변경 전

```bash
singainnn6931@c4r2s5 2_Permission % ls -l default_file
-rw-r--r-- 1 singainnn6931 singainnn6931 0 Jul 30 14:09 default_file
```

### 파일 권한 권한 변경

```bash
singainnn6931@c4r2s5 2_Permission % chmod 777 default_file
```

### 파일 권한 변경 후

```bash
singainnn6931@c4r2s5 2_Permission % ls -l default_file
-rwxrwxrwx 1 singainnn6931 singainnn6931 0 Jul 30 14:09 default_file
```

---

### 디렉터리 권한 변경 전

```bash
singainnn6931@c4r2s5 2_Permission % ls -ld default_directory
drwxr-xr-x 2 singainnn6931 singainnn6931 64 Jul 30 14:09 default_directory
```

### 디렉터리 권한 변경

```bash
singainnn6931@c4r2s5 2_Permission % chmod 000 default_directory
```

### 디렉터리 변경 후

```bash
singainnn6931@c4r2s5 2_Permission % ls -ld default_directory
d--------- 2 singainnn6931 singainnn6931 64 Jul 30 14:09 default_directory
```

</details>


## `chmod` 문자 표기법
- 문자(Symbolic Mode)를 사용하여 특정 사용자에게 권한을 추가하거나 제거하는 방식

``` bash
chmod [대상][연산자][권한] [파일 또는 디렉터리]
```

### 대상

| 문자 | 의미 |
| :---: | :--- |
| `u` | 소유자(Owner) |
| `g` | 그룹(Group) |
| `o` | 기타 사용자(Other) |
| `a` | 모든 사용자(All = `u` + `g` + `o`) |

### 연산자

| 기호 | 의미 |
| :---: | :--- |
| `+` | 권한 추가 |
| `-` | 권한 제거 |
| `=` | 기존 권한을 지정한 권한으로 설정 |

### 권한

| 문자 | 의미 |
| :---: | :--- |
| `r` | 읽기(Read) |
| `w` | 쓰기(Write) |
| `x` | 실행(Execute) |

<details>
<summary>실행 결과</summary>

### 변경 전

```bash
singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  1643 Jul 30 14:21 Permission_Command.md
d---------  2 singainnn6931  singainnn6931    64 Jul 30 14:09 default_directory
-rwxrwxrwx  1 singainnn6931  singainnn6931     0 Jul 30 14:09 default_file
```

### 권한 변경

```bash
# 디렉터리의 소유자에게 읽기, 쓰기, 실행 권한 추가
singainnn6931@c4r2s5 2_Permission % chmod u+rwx default_directory

# 파일의 그룹 권한 제거
singainnn6931@c4r2s5 2_Permission % chmod g-rwx default_file

# 파일의 기타 사용자 읽기 및 실행 권한 제거
singainnn6931@c4r2s5 2_Permission % chmod o-rx default_file
```

### 변경 후

```bash
singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  1643 Jul 30 14:21 Permission_Command.md
drwx------  2 singainnn6931  singainnn6931    64 Jul 30 14:09 default_directory
-rwx----w-  1 singainnn6931  singainnn6931     0 Jul 30 14:09 default_file
```

</details>

## chmod -R
- `-R`(Recursive) 옵션은 **디렉터리와 그 안의 모든 하위 디렉터리 및 파일의 권한을 재귀적으로 변경**한다

```bash
chmod -R [권한] [디렉터리]
```

<details>
<summary>실행 결과</summary>

### 변경 전

```bash
singainnn6931@c4r2s5 2_Permission % ls -l default_directory
total 0
drwxr-xr-x  2 singainnn6931  singainnn6931  64 Jul 30 14:34 testdir
-rw-r--r--  1 singainnn6931  singainnn6931   0 Jul 30 14:34 testfile
```

### 권한 변경

```bash
singainnn6931@c4r2s5 2_Permission % chmod -R 777 default_directory
```

### 변경 후

```bash
singainnn6931@c4r2s5 2_Permission % ls -l default_directory
total 0
drwxrwxrwx  2 singainnn6931  singainnn6931  64 Jul 30 14:34 testdir
-rwxrwxrwx  1 singainnn6931  singainnn6931   0 Jul 30 14:34 testfile
```

</details>

## umask
- "User Mask"의 줄임말로, 리눅스 및 유닉스 시스템에서 새로운 파일이나 디렉토리가 생성될 때 기본 권한(Permission)을 결정(제한)하는 값입니다.
- 디렉토리의 최대 기본 권한: 777 (rwxrwxrwx) — 진입 및 탐색을 위해 실행(x) 권한 필수
- 파일의 최대 기본 권한: 666 (rw-rw-rw-) — 실행 파일이 아니므로 보안상 기본 실행(x) 권한 제외

``` bash
계산 공식 (개념적)

최종 디렉토리 권한 = 777 - umask = 755

최종 파일 권한 = 666 - umask = 644
```

## chown
- 파일이나 디렉터리의 **소유자(Owner)** 또는 **소유 그룹(Group)**을 변경하는 명령어이다.
리눅스 시스템은 보안을 위해 새로 만드는 파일과 디렉토리에 대해 최대 기본 권한(부모 권한)을 정해두고 있습니다.

``` bash
chown [옵션] [새 소유자]:[새 그룹] [파일/디렉토리명]
```

``` bash
# 1. 소유자만 변경
sudo chown alice script.sh

# 2. 소유자와 소유 그룹을 동시에 변경
sudo chown alice:developers script.sh

# 3. 소유자는 바꾸고, 소유자의 기본 그룹으로 자동 설정 (그룹명 생략)
sudo chown alice: script.sh

# 4. 하위 모든 파일/디렉토리 소유권 일괄 변경 (-R 옵션)
sudo chown -R alice:developers /var/www/html
```

## chgrp
- 파일의 소유 그룹만 변경하는 전용 명령어입니다.

``` bash
chgrp [옵션] [새 그룹] [파일/디렉토리명]
```

``` bash
# 1. 소유 그룹 변경
sudo chgrp developers project.txt

# 2. 하위 모든 파일/디렉토리의 소유 그룹 일괄 변경 (-R 옵션)
sudo chgrp -R developers /var/www/html
```

## id
- 현재 로그인한 사용자의 사용자 ID(uid), 그룹 ID(gid), 소속 그룹 정보를 확인한다.
```bash
singainnn6931@c4r2s5 2_Permission % id
uid=1267601098(singainnn6931) gid=1267601098(singainnn6931) groups=1267601098(singainnn6931),12(everyone),62(netaccounts),1267600004(students),1267601067(codyssey_allinone_2nd_2026),701(com.apple.sharepoint.group.1),703(com.apple.sharepoint.group.3),705(com.apple.sharepoint.group.5),704(com.apple.sharepoint.group.4),702(com.apple.sharepoint.group.2)
```

### 출력 항목

|항목|설명|
|---|---|
|`uid`|사용자(User)의 고유 ID|
|`gid`|기본 그룹(Group)의 고유 ID|
|`groups`|현재 사용자가 속한 그룹 목록|


## stat
- 파일이나 디렉터리의 상세 정보를 확인한다.
- 권한, 크기, 소유자, 생성·수정 시간을 확인할 때 사용한다.
```bash
stat [옵션] <파일 또는 디렉터리>
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 2_Permission % stat default_file
16777231 67529866 -rwx----w- 1 singainnn6931 staff 0 0 "Jul 30 14:09:37 2026" "Jul 30 14:09:37 2026" "Jul 30 14:21:18 2026" "Jul 30 14:09:37 2026" 4096 0 0 default_file
```
</details>

### 확인 가능한 정보
|항목|설명|
|---|---|
|파일 종류|일반 파일, 디렉터리 등|
|권한(Permission)|`rwx` 형태의 접근 권한|
|소유자(Owner)|파일 소유 사용자|
|그룹(Group)|파일 소유 그룹|
|크기(Size)|파일 크기(Byte)|
|시간(Time)|생성, 수정, 접근 시간|
