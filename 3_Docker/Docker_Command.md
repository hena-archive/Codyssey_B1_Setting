# 도커 명령어
- [x] 시스템 & 정보 확인
  - [x] docker version
  - [x] docker info

- [x] 시스템 정리
  - [x] docker system prune

- [x] 도커 이미지 명령어
  - [x] docker images 
  - [x] docker pull
  - [x] docker build
  - [x] docker rmi
  - [x] docker history

- [x] 컨테이너 라이프사이클 관리
  - [x] docker run
  - [x] docker ps
  - [x] docker stop
  - [x] docker start
  - [x] docker restart
  - [x] docker rm

- [x] 컨테이너 내부 동작 & 접속
  - [x] docker exec
  - [x] docker logs

- [x] 컨테이너 상태 & 모니터링
  - [x] docker inspect
  - [x] docker top
  - [x] docker stats

## Docker 동작 흐름

```text
Dockerfile
            │
            ▼
docker build
            │
            ▼
Image
            │
docker run
            ▼
Container

## 시스템 & 정보 확인 명령어
### 도커 버전 확인 명령어
- `docker --version` : Docker CLI(Client)의 버전만 간단하게 확인합니다.
- `docker version` : Docker Client와 Docker Engine(Server)의 상세 정보를 함께 출력합니다.

```bash
docker --version

docker version
```
<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker --version
Docker version 28.5.2, build ecc6942

singainnn6931@c4r2s5 3_Docker % docker version
Client:
 Version:           28.5.2
 API version:       1.51
 Go version:        go1.25.3
 Git commit:        ecc6942
 Built:             Wed Nov  5 14:42:30 2025
 OS/Arch:           darwin/amd64
 Context:           orbstack

Server: Docker Engine - Community
 Engine:
  Version:          28.5.2
  API version:      1.51 (minimum version 1.24)
  Go version:       go1.24.9
  Git commit:       89c5e8f
  Built:            Wed Nov  5 14:45:42 2025
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v2.2.0
  GitCommit:        1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc:
  Version:          1.3.3
  GitCommit:        d842d7719497cc3b774fd71620278ac9e17710e0
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```
</details>

### 도커 엔진의 전반적인 상태 확인 명령어
``` bash
docker info
```

<details>
<summary>실행 결과</summary>

```bash
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/singainnn6931/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/singainnn6931/.docker/cli-plugins/docker-compose

Server:
 Containers: 1
  Running: 1
  Paused: 0
  Stopped: 0
 Images: 2
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 6ad9eea8-8821-4f02-99d9-6fd7204eb6fc
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```
</details>

### 시스템 전체 리소스 정리
- 사용하지 않는 미사용(Unused) 리소스들을 한 번에 청소해주는 명령어
- 볼륨(Volume)은 기본적으로 삭제되지 않음
- `-a` (또는 `--all`) : 이름 없는(Dangling) 이미지뿐만 아니라, 현재 어떤 컨테이너에서도 사용하지 않는 모든 이미지를 전부 삭제
- `--volumes` : 컨테이너에 연결되어 있지 않은 미사용 볼륨(Volume)까지 함께 삭제
- `-f` (또는 `--force`) : [y/N] 확인 절차 없이 즉시 강제로 정리를 진행
``` bash
docker system prune
```


``` bash
singainnn6931@c4r2s5 3_Docker % docker system prune
WARNING! This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images
  - unused build cache

Are you sure you want to continue? [y/N] y
Deleted Containers:
034050120b8128f96de093acb48ed3178fc95f3df2dbd4e15b72ae2e3032880b
4b980fb6d4de82a83d18240fe329f059ed7d8ea6c5af009cdf7b51e2bb637ee5
6f60dac90869074bafc1e7ffd519c145abb85d3c167b899aa2f82b1f5c3ae29f

Deleted build cache objects:
xeszwnpebqlz297pczd20mct3
qdxgyiq7fjv8gjtd8dmhebgcc
vzl7phjuoimzvo74yuzekyda2
tpq6cyaaytaoxjpeny6rv0a4v
jd9tuukdcuff4y9r4dxwhfj3m
63s1glv299pw1vp7ebkfrgzsf
8bj41y2hlxjputef7isop46rl
tmeeijnl638z5m0fod5z2rw17
la6dbh8if0bjcfy70nkviosa6
rspuh0scdnllxn7fwjdr2tvlw

Total reclaimed space: 576.8kB
```

## 도커 이미지

### 도커 이미지 확인 명령어
- 로컬 시스템(내 컴퓨터)에 다운로드되어 있거나 직접 빌드한 도커 이미지 목록을 확인할 때 사용
- `-a` : 중간 레이어 이미지까지 포함하여 모든 이미지 출력
- `-q` : 다른 명령어와 조합해서 쓸 때 유용한 Image ID만 추출하는 옵션
```bash
docker images
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    4e5db4761e0f   2 weeks ago   161MB
```
- REPOSITORY: 이미지 이름 (예: ubuntu, nginx, my-app)
- TAG: 이미지 버전 (태그를 지정하지 않으면 기본값은 latest)
- IMAGE ID: 이미지의 고유 식별자 (12자리 해시값)
- CREATED: 이미지가 생성된 시점
- SIZE: 이미지의 실제 용량

### 도커 이미지 다운로드 명령어
``` bash
docker pull <image>
```
- 태그를 명시하지 않으면 자동으로 최신 버전 다운

``` bash
singainnn6931@c4r2s5 A_WebServer % docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:5a88c9c45479443d7be2eadc894b4ed0a9801bae03d97a5760ae13b5c2005942
Status: Image is up to date for nginx:latest
docker.io/library/nginx:latest
```

### 도커 이미지 빌드 명령어
- 사용자가 작성한 Dockerfile 문서의 설정 내용을 바탕으로 새로운 도커 이미지를 직접 생성할 때 사용
- `-t` : 이미지 이름 및 태그 지정
``` bash
docker build -t <name> .
```

### 도커 이미지 삭제 명령어
- 더 이상 사용하지 않는 로컬 이미지를 삭제
- 컨테이너 삭제 우선: 해당 이미지를 기반으로 생성된 컨테이너가 하나라도 존재하면(중지된 상태 포함) 삭제되지 않고 오류가 발생
- `-f` : 컨테이너 존재 여부와 관계없이 강제로(Force) 삭제
```bash
docker rmi <image>
```

``` bash
# 태그로 삭제
docker rmi ubuntu:22.04
# 또는 Image ID로 삭제
docker rmi a1b2c3d4e5f6
```


### 이미지 히스토리 확인 명령어
- 해당 이미지가 어떤 단계(Dockerfile 명령어들)를 거쳐 만들어졌는지 빌드 이력을 확인
- `--no-trunc` : 길어서 생략된(...) 빌드 명령어 원본 전체를 잘림 없이 출력
``` bash
docker history <image>
```
확인 가능 항목:
- 각 레이어가 생성될 때 실행된 명령어 (RUN, COPY, EXPOSE 등)
- 각 레이어가 차지하는 용량
- 이미지에 보안상 불필요한 레이어가 포함되어 있는지 확인할 때 유용합니다.


## 컨테이너 라이프사이클 관리
### 컨테이너 생성 및 실행 명령어
- 이미지를 바탕으로 새로운 컨테이너를 생성하고 백그라운드/포그라운드로 실행
- 로컬에 이미지가 없다면 자동으로 Docker Hub에서 pull 후 실행
- `-d` : 백그라운드 모드 실행 (데몬 형태)
- `-p` : 호스트와 컨테이너 간 포트 포워딩 설정 (<호스트 포트>:<컨테이너 포트>)
- `--name` : 컨테이너에 고유한 이름 부여
- `-v` : 호스트 디렉토리와 컨테이너 내부 디렉토리 바인딩 (볼륨 마운트)
- `-it` : 터미널 입출력 활성화 (-i interactive + -t tty)
- `--rm` : 컨테이너 종료 시 자동 삭제

```Bash
docker run [옵션] <image> [command]
```

```Bash
singainnn6931@c4r2s5 A_WebServer % docker run -d -p 8080:80 --name my-web nginx
4f2e91a0c8b3d4e5f6a7b8c9d0e1f2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9
```


### 컨테이너 목록 조회 명령어
- 현재 실행 중이거나 정지된 컨테이너 목록을 확인
- `-a` : 정지되거나 종료된 컨테이너를 포함하여 모든 컨테이너 출력
- `-q` : 다른 명령어와 조합해서 쓸 때 유용한 Container ID만 추출하는 옵션

```bash 
docker ps
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                  NAMES
4f2e91a0c8b3   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->80/tcp   my-web
```
상태 분석
- CONTAINER ID: 컨테이너의 고유 식별자 (12자리 해시값)
- IMAGE: 컨테이너 생성에 사용된 베이스 이미지
- COMMAND: 컨테이너 시작 시 실행되는 프로세스/명령어
- CREATED: 컨테이너가 생성된 시점
- STATUS: 현재 컨테이너 상태 (Up, Exited, Created 등)
- PORTS: 포트 포워딩 설정 정보
- NAMES: 지정했거나 자동으로 생성된 컨테이너 이름

### 컨테이너 정지 명령어
- 실행 중인 컨테이너를 안전하게 종료
- SIGTERM 신호를 보내 작업을 정리하도록 대기한 후 안전하게 정지

``` bash
docker stop <container>
```

``` bash
# 이름으로 정지
singainnn6931@c4r2s5 A_WebServer % docker stop my-web
my-web

# 또는 Container ID로 정지
singainnn6931@c4r2s5 A_WebServer % docker stop 4f2e91a0c8b3
4f2e91a0c8b3
```
0
### 컨테이너 재실행 명령어
- docker stop으로 정지된 기존 컨테이너를 다시 시작
- docker run과 달리 새로운 컨테이너를 생성하지 않고 기존 컨테이너를 재가동


``` bash
docker start <container>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker start my-web
my-web
```

### 컨테이너 재시작 명령어
- 실행 중이거나 정지된 컨테이너를 정지 후 즉시 다시 시작
- 애플리케이션 프로세스 재부팅이나 설정 반영 시 활용

``` bash
docker restart <container>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker restart my-web
my-web
```

### 컨테이너 삭제 명령어
- 더 이상 사용하지 않는 컨테이너를 완전히 삭제
- 컨테이너 정지 우선: 실행 중인 컨테이너는 삭제되지 않으며 먼저 docker stop으로 정지해야 함
- `-f` : 실행 중인 컨테이너도 강제로(Force) 정지 후 삭제
- `-v` : 컨테이너와 연결된 익명 볼륨도 함께 삭제

``` bash
docker rm <container>
```

``` bash
# 컨테이너 정지 후 삭제
singainnn6931@c4r2s5 A_WebServer % docker stop my-web
my-web
singainnn6931@c4r2s5 A_WebServer % docker rm my-web
my-web

# 정지된 모든 컨테이너 일괄 삭제
singainnn6931@c4r2s5 A_WebServer % docker rm $(docker ps -a -q)
```

## 컨테이너 내부 접속 & 모니터링
### 컨테이너 내부 명령어 실행 (내부 접속)
- 실행 중인 컨테이너 내부에서 새로운 명령어를 실행할 때 사용 (주로 bash/sh 쉘 접속 시 활용)
- `-i` : 표준 입출력(STDIN)을 열어 두어 대화형 모드 유지
- `-t` : 가상 터미널(TTY)을 할당하여 실제 셸 환경처럼 동작하게 설정
- `-u` : 특정 사용자 계정으로 명령 실행 (예: -u root)

``` bash
docker exec [옵션] <container> <command>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker exec -it my-web bash
root@4f2e91a0c8b3:/# nginx -v
nginx version: nginx/1.25.3
root@4f2e91a0c8b3:/# exit
exit
```

### 컨테이너 로그 조회 명령어
- 컨테이너 내부의 메인 프로세스(STDOUT / STDERR)가 출력한 로그를 확인
- `-f` : 실시간으로 출력되는 로그를 계속 모니터링 (follow)
- `-t` : 로그 출력 시 해당 시점의 타임스탬프 함께 표시 (timestamps)
- `--tail` : 출력할 마지막 로그 줄 수 지정 (예: --tail 100)

``` bash
docker logs [옵션] <container>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker logs -f --tail 5 my-web
2026/08/02 18:00:12 [notice] 1#1: start worker process 29
172.17.0.1 - - [02/Aug/2026:18:01:05 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0"
172.17.0.1 - - [02/Aug/2026:18:01:06 +0000] "GET /favicon.ico HTTP/1.1" 404 153 "-" "Mozilla/5.0"
```


### 컨테이너/이미지 상세 정보 조회 명령어
- 컨테이너 또는 이미지의 모든 설정값과 상태 정보를 JSON 형태로 출력
- `-f` : Go 템플릿 문법을 사용하여 특정 키값만 추출 출력 (format)
- `--type` : 동일한 이름의 이미지와 컨테이너가 존재할 때 대상 유형 명시 (container 또는 image)

``` bash
docker inspect [옵션] <container|image>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker inspect -f '{{.NetworkSettings.IPAddress}}' my-web
172.17.0.2
```

### 컨테이너 프로세스 조회 명령어
- 실행 중인 특정 컨테이너 내부에서 동작하고 있는 프로세스 목록을 확인
- 호스트 시스템에서 본 컨테이너 내부 프로세스의 PID와 실행 명령어를 확인 시 유용
``` bash
docker top <container>
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker top my-web
UID         PID         PPID        C           STIME       TTY         TIME        CMD
root        10234       10210       0           18:00       ?           00:00:00    nginx: master process nginx -g daemon off;
101         10280       10234       0           18:00       ?           00:00:00    nginx: worker process
```

### 컨테이너 리소스 사용량 모니터링 명령어
- 실행 중인 컨테이너들의 CPU, 메모리, 네트워크 I/O, 디스크 I/O 사용량을 실시간 스트리밍으로 확인
- `--no-stream` : 실시간 갱신 없이 실행 시점의 단일 결과만 출력 후 종료
- `-a` : 정지된 컨테이너까지 포함하여 리소스 현황 확인

``` bash
docker stats [옵션] [container...]
```

``` bash
singainnn6931@c4r2s5 A_WebServer % docker stats --no-stream my-web
CONTAINER ID   NAME     CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O   PIDS
4f2e91a0c8b3   my-web   0.01%     3.58MiB / 7.67GiB     0.05%     1.02kB / 682B   0B / 0B     2
```