# 터미널 명령어 리스트
- [x] 현재 위치 확인
  - [x] pwd 
- [x] 목록 확인(숨김 파일 포함)
  - [x] ls
  - [x] -a 옵션
  - [x] -l 옵션
- [x] 이동
  - [x] cd 
  - [x] ~
  - [x] -
  - [x] /
  - [x] ..
  
- [x] 생성
  - [x] mkdir
  - [x] touch 
- [x] 복사
  - [x] cp 
- [x] 이동 / 이름 변경
  - [x] mv 
- [x] 삭제
  - [x] rm 
- [x] 파일 내용 확인
  - [x] cat
  - [x] head
  - [x] tail
  - [x] less
- 빈 파일 생성

## 현재 위치 확인 명령어
- 현재 작업 중인 디렉터리(폴더)의 전체 경로를 출력

``` bash
pwd
```

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % pwd
/Users/singainnn6931/Codyssey/Basic/1_Setting/1_Terminal
```
</details>

## 목록 확인 명령어
- 현재 디렉터리의 파일과 폴더를 확인
  - `-l` : 상세 정보 출력
  - `-a` : 숨김 파일(.으로 시작하는 파일)까지 출력

``` bash
ls
```

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md

singainnn6931@c4r2s5 1_Terminal % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  324 Jul 30 13:28 Terminal_Command.md

singainnn6931@c4r2s5 1_Terminal % ls -a
.			..			Terminal_Command.md

singainnn6931@c4r2s5 1_Terminal % ls -al
total 40
drwxr-xr-x  6 singainnn6931  singainnn6931   192 Aug  2 14:20 .
drwxr-xr-x  5 singainnn6931  singainnn6931   160 Aug  2 13:55 ..
-rw-r--r--  1 singainnn6931  singainnn6931  5058 Aug  2 14:31 Terminal_Command.md
```
</details>

## 이동 명령어
- 원하는 디렉터리로 이동
  - `폴더 이름` : 폴더 안의 하위 폴더로 이동
  - `..` : 상위 디렉토리로 이동
  - `/` : 루트 디렉토리로 이동
  - `~` : 내 계정의 기본 홈 폴더로 이동
  - `-` : 이전 폴더로 돌아가기

- 절대 경로: 최상위 디렉토리 기준
- 상대 경로: 현재 파일의 위치를 기준


``` bash
cd
```

<details>
<summary>실행 결과</summary>

``` bash
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

## 생성 명령어 (mkdir, touch)
### 새로운 디렉토리 생성
- mkdir : 새로운 디렉터리 생성

``` bash
mkdir 폴더 이름
```

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % mkdir newDirectory
singainnn6931@c4r2s5 1_Terminal % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  932 Jul 30 13:37 Terminal_Command.md
drwxr-xr-x  2 singainnn6931  singainnn6931   64 Jul 30 13:41 newDirectory
```
</details>


### 새로운 파일 생성
- touch : 새로운 파일 생성
``` bash
touch 파일 이름
```
<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % touch newFile.txt
singainnn6931@c4r2s5 1_Terminal % ls -l
total 8
-rw-r--r--  1 singainnn6931  singainnn6931  932 Jul 30 13:37 Terminal_Command.md
-rw-r--r--  1 singainnn6931  singainnn6931    0 Jul 30 13:41 newFile.txt
```
</details>

## 복사 명령어 
- 파일 또는 디렉터리를 복사
- 디렉터리는 -r 옵션을 사용

``` bash
cp 복사할_파일 파일_이름
``` 

<details>
<summary>실행 결과</summary>

``` bash
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
- 파일이나 폴더의 위치를 변경하거나 이름을 변경

<details>
<summary>실행 결과</summary>

``` bash
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
- rm : 파일 삭제
  - `-r` : 디렉터리 삭제 옵션

### rmdir 명령어
- rmdir : 비어 있는 디렉터리 삭제

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % ls
Terminal_Command.md	newDirectory1		newFile.txt
newDirectory		newDirectory2		newFile1.txt

# 파일 삭제지만 가능
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
- 파일 전체 내용을 출력
``` bash
cat file_name
```

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 1_Terminal % echo "hello world" > Test.txt 
singainnn6931@c4r2s5 1_Terminal % cat Test.txt 
hello world
```
</details>



### head 명령어
- 파일 앞부분 확인
- 기본 10줄 출력
  - n옵션으로 개수 조절 가능

``` bash
head 파일명
```

### tail 명령어
- 파일 뒷부분 확인
- 기본 10줄 출력
  - n옵션으로 개수 조절 가능
- 로그 확인할 때 많이 사용
  - `-f` 온션으로 실시간 확인 가능


``` bash
tail 파일명
```


```
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

### less 명령어
- 긴 파일을 페이지 단위로 출력

|키|기능
|------|---|
|Space|다음 페이지|
|↑ ↓|스크롤|
|q|종료|
|page up / down|한 페이지씩 이동|
|home / end|끝 지점으로 이동|