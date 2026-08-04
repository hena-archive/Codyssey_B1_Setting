# 권한 체크 리스트
- [x] 권한
- [x] chmod 숫자
  - 숫자
  -  문자
  -  `-R` 
 
- [x] umask

- [x] chown

- [x] chgrp

- [x] id

- [x] stat

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

## 권한
- 사용자가 컴퓨터 시스템에서 파일, 프로그램, 장치 등의 자원을 보거나, 바꾸거나, 실행할 수 있는 허락의 단계
- 파일 소유자 (Owner): 파일을 처음 만든 주인입니다. 내가 만든 파일이므로 그룹이나 아더에게 권한을 줄지 말지 스스로 결정할 수 있습니다.
- 최고 관리자 (Root / Administrator): 시스템의 절대 권한자입니다. 소유자가 누구든 상관없이 모든 파일의 권한을 강제로 바꿀 수 있습니다.


```bash
-   rwx   rwx   rwx
│    │     │     │
│    │     │     └── 기타 사용자(Other)
│    │     └──────── 그룹(Group)
│    └────────────── 소유자(Owner)
└─────────────────── 파일 종류
```

### 파일 종류
|문자|의미|
|--|--|
| - |일반 파일|
|d|디렉토리|
|l|심볼릭 링크|


### 권한 종류
|문자|의미|
|--|--|
| r | 읽기 |
| w | 쓰기 |
| x | 실행 |
| - | 없음 |

## chmod 숫자 표기법

``` bash
chmod [권한(3자리 숫자)] [파일 또는 디렉터리]
```

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

``` bash
# 파일 권한 변경
singainnn6931@c4r2s5 2_Permission % chmod 777 default_file

singainnn6931@c4r2s5 2_Permission % ls -l 
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  568 Jul 30 14:10 Permission_Command.md
drwxr-xr-x  2 singainnn6931  singainnn6931   64 Jul 30 14:09 default_directory
-rwxrwxrwx  1 singainnn6931  singainnn6931    0 Jul 30 14:09 default_file

# 디렉토리 권한 변경
singainnn6931@c4r2s5 2_Permission % chmod 000 default_directory

singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  568 Jul 30 14:10 Permission_Command.md
d---------  2 singainnn6931  singainnn6931   64 Jul 30 14:09 default_directory
-rwxrwxrwx  1 singainnn6931  singainnn6931    0 Jul 30 14:09 default_file
```
</details>

## chmod 문자 표기법
- u(owner)
- g(group)
- o(other)

``` bash
chmod 그룹종류 + or - 권한 파일이름
```

``` bash
singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  1643 Jul 30 14:21 Permission_Command.md
d---------  2 singainnn6931  singainnn6931    64 Jul 30 14:09 default_directory
-rwxrwxrwx  1 singainnn6931  singainnn6931     0 Jul 30 14:09 default_file

# 디렉토리의 유저 권한 read, write, excute 권한 부여
singainnn6931@c4r2s5 2_Permission % chmod u+rwx default_directory 

# 파일의 그룹 권한 read, write, excute 권한 제거
singainnn6931@c4r2s5 2_Permission % chmod g-rwx default_file

# 파일의 기타 사용자 권한 read, excute 권한 제거
singainnn6931@c4r2s5 2_Permission % chmod o-rx default_file

singainnn6931@c4r2s5 2_Permission % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  1643 Jul 30 14:21 Permission_Command.md
drwx------  2 singainnn6931  singainnn6931    64 Jul 30 14:09 default_directory
-rwx----w-  1 singainnn6931  singainnn6931     0 Jul 30 14:09 default_file
```

## chmod -R
- 하위 디렉토리 파일들도 바뀜
``` bash
singainnn6931@c4r2s5 2_Permission % sudo chmod -R 000 default_directory
Password:
Sorry, try again.
Password:
singainnn6931 is not in the sudoers file.
This incident has been reported to the administrator.
singainnn6931@c4r2s5 2_Permission % sudo chmod -R 777 default_directory
Password:
sudo: a password is required
singainnn6931@c4r2s5 2_Permission % chmod -R 777 default_directory 
singainnn6931@c4r2s5 2_Permission % cd default_
cd: no such file or directory: default_
singainnn6931@c4r2s5 2_Permission % cd default_directory 
singainnn6931@c4r2s5 default_directory % ls
testdir		testfile
singainnn6931@c4r2s5 default_directory % ls -l
total 0
drwxrwxrwx  2 singainnn6931  singainnn6931  64 Jul 30 14:34 testdir
-rwxrwxrwx  1 singainnn6931  singainnn6931   0 Jul 30 14:34 testfile
```

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
- 파일이나 디렉토리의 소유자를 변경하며, 필요시 소유 그룹까지 한 번에 변경할 수 있어 가장 자주 사용됩니다.
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

## Error
### 문제 상황
```bash
chmod -R 000 default_directory
```
- 실행 시 Permission denied 발생

### 원인
디렉터리에 접근 권한이 없어 권한 변경 명령을 수행할 수 없었다.

### 해결
디렉터리 권한을 복구한 후 다시 chmod를 수행하였다.
