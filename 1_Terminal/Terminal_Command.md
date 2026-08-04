# 터미널 조작 기초


## 터미널 명령어 체크 리스트
- [x] 현재 위치 확인
  - [x] pwd 

- [x] 목록 확인(숨김 파일 포함)
  - [x] ls

- [x] 이동
  - [x] cd

- [x] 디렉토리 생성 및 빈 파일 생성
  - [x] mkdir
  - [x] touch 

- [x] 복사
  - [x] cp 

- [x] 이동 / 이름 변경
  - [x] mv 

- [x] 삭제
  - [x] rm 
  - [x] rmdir 

- [x] 파일 내용 확인
  - [x] cat
  - [x] head
  - [x] tail
  - [x] less

## 현재 위치 확인 명령어 (pwd)
- 현재 작업 디렉터리(Working Directory)의 절대 경로(Absolute Path)를 출력하는 명령어이다.

```bash
pwd
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % pwd 
/Users/singainnn6931/1_Setting/1_Terminal
```

</details>

## 목록 확인 명령어 (ls)
- 현재 작업 디렉터리에 있는 파일과 디렉터리의 목록을 출력하는 명령어이다.

```bash
ls [옵션] [파일 또는 디렉터리]
```

- **파일 또는 디렉터리** : 목록을 확인할 대상이다. 생략하면 현재 작업 디렉터리를 대상으로 한다.

### 주요 옵션


| 옵션 | 설명 |
| :--- | :--- |
| `-l` | 파일 및 디렉터리의 권한, 소유자, 크기, 수정 시간 등을 **긴 형식(Long Format)**으로 출력한다. |
| `-a` | `.`으로 시작하는 **숨김 파일 및 숨김 디렉터리**를 포함하여 출력한다. |
| `-al` 또는 `-la` | `-a`와 `-l` 옵션을 함께 적용하여 **숨김 파일을 포함한 상세 정보**를 출력한다. |


<details>
<summary>ls 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % ls
Korean_national_anthem.txt	Terminal_Command.md
long.txt
```

</details>

<details>
<summary>ls -l 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % ls -l
total 32
-rw-r--r--  1 singainnn6931  singainnn6931   704  8  3 13:34 Korean_national_anthem.txt
-rw-r--r--  1 singainnn6931  singainnn6931   692  8  3 13:34 long.txt
-rw-r--r--  1 singainnn6931  singainnn6931  8160  8  5 03:19 Terminal_Command.md
```

</details>

<details>
<summary>ls -a 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % ls -a
.				long.txt
..				Terminal_Command.md
Korean_national_anthem.txt
```

</details>

<details>
<summary>ls -al 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % ls -al
total 40
drwxr-xr-x   5 singainnn6931  singainnn6931   160  8  3 13:34 .
drwxr-xr-x  10 singainnn6931  singainnn6931   320  8  4 19:22 ..
-rw-r--r--   1 singainnn6931  singainnn6931   704  8  3 13:34 Korean_national_anthem.txt
-rw-r--r--   1 singainnn6931  singainnn6931   692  8  3 13:34 long.txt
-rw-r--r--   1 singainnn6931  singainnn6931  8488  8  5 03:25 Terminal_Command.md
```

</details>


## 이동 명령어 (cd)
- 현재 작업 디렉터리를 다른 디렉터리로 변경하는 명령어이다.
- 절대 경로와 상대 경로를 모두 사용할 수 있으며, 다양한 경로를 이용해 원하는 디렉터리로 이동할 수 있다.
  - 절대 경로: 루트 디렉터리( `/` )부터 시작하는 전체 경로
  - 상대 경로: 현재 작업 중인 디렉터리를 기준으로 하는 경로


```bash
cd [디렉터리]
```

### 주요 사용 방법

| 명령어 | 설명 |
| :--- | :--- |
| `cd 디렉터리명` | 지정한 디렉터리로 이동한다. |
| `cd ..` | 상위 디렉터리로 이동한다. |
| `cd /` | 루트 디렉터리로 이동한다. |
| `cd ~` | 현재 사용자의 홈 디렉터리로 이동한다. |
| `cd -` | 직전에 작업했던 디렉터리로 이동한다. |
| `cd` | 홈 디렉터리로 이동한다. |

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % cd ..
singainnn6931@c4r2s5 1_Setting % 

singainnn6931@c4r2s5 1_Terminal % cd /
singainnn6931@c4r2s5 / % 

singainnn6931@c4r2s5 1_Terminal % cd ~
singainnn6931@c4r2s5 ~ % 

singainnn6931@c4r2s5 ~ % cd -
~/Codyssey/Basic/1_Setting/1_Terminal
singainnn6931@c4r2s5 1_Terminal % 
```
</details>

## 생성 명령어


### 새로운 디렉토리 생성 명령어 (`mkdir`)
- 새로운 디렉터리(폴더)를 생성하는 명령어이다. 

```bash
mkdir [옵션] 디렉터리명
```

### 주요 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-p` | 필요한 상위 디렉터리를 함께 생성한다. |
| `-v` | 생성된 디렉터리의 정보를 출력한다. |

<details>
<summary>mkdir 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % mkdir newDirectory
singainnn6931@c4r2s5 1_Terminal % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  932 Jul 30 13:37 Terminal_Command.md
drwxr-xr-x  2 singainnn6931  singainnn6931   64 Jul 30 13:41 newDirectory
```
</details>


### 새로운 파일 생성 명령어 (`touch`)
- 새로운 빈 파일을 생성하며, 기존 파일이 존재하면 수정 시간을 갱신한다.

```bash
touch 파일명
```
<details>
<summary>touch 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % touch newFile.txt
singainnn6931@c4r2s5 1_Terminal % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  932 Jul 30 13:37 Terminal_Command.md
-rw-r--r--  1 singainnn6931  singainnn6931    0 Jul 30 13:41 newFile.txt
```

</details>

## 복사 명령어 (cp)
- 파일이나 디렉터리를 다른 위치로 복사하거나 새로운 이름으로 복사하는 명령어이다.

```bash
cp [옵션] [원본] [대상]
```

### 주요 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-r` | 디렉터리와 그 하위 파일 및 디렉터리를 재귀적으로 복사한다. |

<details>
<summary>cp 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % cp newFile.txt newFile1.txt
singainnn6931@c4r2s5 1_Terminal % cp newDirectory newDirectory1
cp: newDirectory is a directory (not copied).
singainnn6931@c4r2s5 1_Terminal % cp -r newDirectory newDirectory1
singainnn6931@c4r2s5 1_Terminal % cd newDirectory
singainnn6931@c4r2s5 newDirectory % touch qwer
singainnn6931@c4r2s5 newDirectory % cd ..
singainnn6931@c4r2s5 1_Terminal % cp -r newDirectory newDirectory2
singainnn6931@c4r2s5 1_Terminal % cd newDirectory2
singainnn6931@c4r2s5 newDirectory2 % ls
qwer
```

</details>

## 이동 / 이름 변경 (mv) 명령어
- 파일이나 디렉터리를 다른 위치로 이동하거나 이름을 변경하는 명령어이다.
- 같은 디렉터리에서 사용하면 이름이 변경되고, 다른 디렉터리를 대상으로 사용하면 해당 위치로 이동한다.

```bash
mv [원본] [대상]
```

<details>
<summary>mv 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % touch trash
singainnn6931@c4r2s5 1_Terminal % ls 
Terminal_Command.md	newDirectory		newFile.txt		trash

# 파일 이름 변경
singainnn6931@c4r2s5 1_Terminal % mv trash trash1
singainnn6931@c4r2s5 1_Terminal % mv newDirectory newDirectory_
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory_		newFile.txt		trash1

# 파일 이동
singainnn6931@c4r2s5 1_Terminal % mv trash1 newDirectory_ 
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory_		newFile.txt

# 옮겨진 파일 확인
singainnn6931@c4r2s5 1_Terminal % ls newDirectory_ 
qwer	trash1
```
</details>

## 삭제 명령어


### rm 명령어
- 파일을 삭제하는 명령어이다.
  - `-r` : 디렉터리 삭제 옵션

```bash
rm [옵션] [파일 또는 디렉터리]
rmdir [디렉터리]
```

### 주요 옵션

| 명령어 | 옵션 | 설명 |
| :--- | :--- | :--- |
| `rm` | `-r` | 디렉터리와 내부의 파일 및 하위 디렉터리를 재귀적으로 삭제한다. |
| `rm` | `-f` | 삭제 여부를 묻지 않고 강제로 삭제한다. |


### rmdir 명령어
- 비어 있는 디렉터리만 삭제할 수 있는 명령어이다.

```bash
rmdir [디렉터리]
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory1		newFile.txt
newDirectory		newDirectory2		newFile1.txt

# 파일 삭제 (`-r` 옵션은 파일에도 사용할 수 있지만 불필요함)
singainnn6931@c4r2s5 1_Terminal % rm -r newFile1.txt
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory1		newFile.txt
newDirectory		newDirectory2

# 내부에 존재하는 디렉토리 삭제 시도
singainnn6931@c4r2s5 1_Terminal % rmdir newDirectory2
rmdir: newDirectory2: Directory not empty

# 빈 디렉토리 삭제 시도
singainnn6931@c4r2s5 1_Terminal % rmdir newDirectory1

# 내부에 파일이 존재하는 디렉토리 삭제 시도
singainnn6931@c4r2s5 1_Terminal % rm -r newDirectory2
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory		newFile.txt
```

</details>

## 파일 내용 확인 명령어


### cat 명령어
- 파일의 전체 내용을 출력하는 명령어이다.
```bash
cat [파일명]
```

<details>
<summary>cat 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % echo "hello world" > Test.txt 
singainnn6931@c4r2s5 1_Terminal % cat Test.txt 
hello world
```

</details>


### head 명령어
- 파일의 앞부분을 출력하는 명령어이다.
- 기본적으로 처음 **10줄**을 출력한다.

```bash
head [옵션] [파일명]
```

### 주요 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-n` | 출력할 줄 수를 지정한다. |


<details>
<summary>head 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % head long.txt 
1
2
3
4
5
6
7
8
9
10
```

</details>

### tail 명령어
- 파일의 마지막 부분을 출력하는 명령어이다.
- 기본적으로 마지막 **10줄**을 출력한다.
- 로그 확인할 때 많이 사용한다.

```bash
tail [옵션] [파일명]
```

### 주요 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-n` | 출력할 줄 수를 지정한다. |
| `-f` | 파일의 변경 사항을 실시간으로 출력한다. |

<details>
<summary>tail 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % tail long.txt
191
192
193
194
195
196
197
198
199
200
```

</details>


<details>
<summary>tail -f 실행 결과</summary>

```bash
tail -f server.log
```

- 파일 변화를 실시간 확인
    - before
        
        ```bash
        191
        192
        193
        194
        195
        196
        197
        198
        199
        200
        ```
        
    - after
        
        ```bash
        191
        192
        193
        194
        195
        196
        197
        198
        199
        200
        201
        ```
        
</details>


### less 명령어
- 긴 파일을 페이지 단위로 조회하는 명령어이다.
- 파일 전체를 한 번에 출력하지 않고 필요한 만큼만 읽을 수 있어 큰 파일을 확인할 때 유용하다.

```bash
less [파일명]
```

<details>
<summary>less 실행 결과</summary>

```bash
singainnn6931@c4r2s5 1_Terminal % less long.txt 
1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
long.txt
```

</details>

### 자주 사용하는 키

| 키 | 기능 |
| :--- | :--- |
| `Space` | 다음 페이지 |
| `↑`, `↓` | 한 줄씩 이동 |
| `Page Up`, `Page Down` | 한 페이지씩 이동 |
| `Home`, `End` | 파일의 처음 또는 끝으로 이동 |
| `q` | 종료 |
