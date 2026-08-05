# 도커 명령어 배우기

## 도커 명령어 체크 리스트
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
  - [x] docker attach
  - [x] docker logs

- [x] 컨테이너 상태 & 모니터링
  - [x] docker inspect
  - [x] docker top
  - [x] docker stats

- [x] 볼륨 관리
  - [x] docker volume create
  - [x] docker volume ls
  - [x] docker volume inspect
  - [x] docker volume rm

- [x] 네트워크
  - [x] docker network ls


## 시스템 & 정보 확인 명령어


### 도커 버전 확인 명령어
- Docker의 설치 여부와 버전을 확인하기 위한 명령어이다.
  - `docker --version` : Docker Client의 버전만 간단하게 확인합니다.
  - `docker version` : Docker Client와 Docker Engine(Server)의 상세 정보를 함께 출력합니다.

```bash
docker --version
```

<details>
<summary>docker --version 실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker --version
Docker version 28.5.2, build ecc6942
```

</details>

```bash
docker version
```

<details>
<summary>docker version 실행 결과</summary>

``` bash
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
- Docker Engine의 현재 실행 상태와 시스템 정보를 확인하는 명령어이다
``` bash
docker info
```

<details>
<summary>docker info 실행 결과</summary>

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
 ...

WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```

</details>

## 시스템 전체 리소스 정리
- Docker에서 **현재 사용하지 않는(Unused) 리소스**를 한 번에 정리하는 명령어이다.
기본적으로 다음 항목을 삭제한다.
- 중지된(Stopped) 컨테이너
- 사용되지 않는 네트워크(Network)
- Dangling 이미지
- 사용하지 않는 빌드 캐시(Build Cache)

> **참고**
>
> Docker 볼륨(Volume)은 기본적으로 삭제되지 않는다.
>
```bash
docker system prune
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-a`, `--all` | Dangling 이미지뿐만 아니라, 현재 어떤 컨테이너에서도 사용하지 않는 모든 이미지를 삭제한다. |
| `--volumes` | 컨테이너에 연결되어 있지 않은 미사용 볼륨까지 함께 삭제한다. |
| `-f`, `--force` | 확인 메시지 없이 즉시 정리를 수행한다. |


<details>
<summary>docker system prune 실행 결과</summary>

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

</details>

## 도커 이미지

### 도커 이미지 확인 명령어
- 로컬 시스템(호스트)에 저장되어 있는 Docker 이미지 목록을 확인하는 명령어이다.
```bash
docker images
```

| 옵션 | 설명 |
| :--- | :--- |
| `-a`, `--all` | 중간 레이어(Intermediate Image)를 포함한 모든 이미지를 출력한다. |
| `-q`, `--quiet` | Image ID만 출력한다. 다른 명령어와 함께 사용할 때 유용하다. |


<details>
<summary>docker images 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    4e5db4761e0f   2 weeks ago   161MB
```

- REPOSITORY: 이미지 이름 (예: ubuntu, nginx, my-app)
- TAG: 이미지 버전 (태그를 지정하지 않으면 기본값은 latest)
- IMAGE ID: 이미지의 고유 식별자 (12자리 해시값)
- CREATED: 이미지가 생성된 시점
- SIZE: 이미지의 실제 용량

</details>


### 도커 이미지 다운로드 명령어
- Docker Hub와 같은 레지스트리(Registry)에서 이미지를 다운로드하는 명령어이다.
- 태그를 명시하지 않으면 자동으로 최신 버전 다운
``` bash
docker pull <image>
```

<details>
<summary>docker pull 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:7f4da0fc94bcece205a8c0b6f4d11c8196924654ffe5c4d1aa439b7f632048b2
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
```

</details>

### 도커 이미지 빌드 명령어
- 사용자가 작성한 Dockerfile 문서의 설정 내용을 바탕으로 새로운 도커 이미지를 직접 생성하는 명령어
``` bash
docker build -t <name> .
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-t`, `--tag` | 이미지 이름과 태그를 지정한다. |
| `-f`, `--file` | 기본 Dockerfile 대신 다른 Dockerfile을 지정한다. |
| `--no-cache` | 캐시를 사용하지 않고 처음부터 새롭게 빌드한다. |

<details>
<summary>docker build 실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker build -t build-test .
[+] Building 0.8s (5/5) FINISHED                                                                                            docker:orbstack
 => [internal] load build definition from dockerfile                                                                                   0.2s
 => => transferring dockerfile: 54B                                                                                                    0.0s
 => [internal] load metadata for docker.io/library/hello-world:latest                                                                  0.0s
 => [internal] load .dockerignore                                                                                                      0.1s
 => => transferring context: 2B                                                                                                        0.0s
 => [1/1] FROM docker.io/library/hello-world:latest                                                                                    0.1s
 => exporting to image                                                                                                                 0.1s
 => => exporting layers                                                                                                                0.0s
 => => writing image sha256:e2ac70e7319a02c5a477f5825259bd118b94e8b02c279c67afa63adab6d8685b                                           0.0s
 => => naming to docker.io/library/build-test                                                                                          0.0s

```

</details>

### 도커 이미지 삭제 명령어
- 로컬 시스템에 저장된 Docker 이미지를 삭제하는 명령어이다.
- 해당 이미지를 사용하는 컨테이너가 하나라도 존재하면(중지된 컨테이너 포함) 삭제되지 않는다.

```bash
docker rmi <image>
```

### 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-f`, `--force` | 이미지를 강제로 삭제한다. |

<details>
<summary>docker rmi 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 ~ % docker rmi build-test
Untagged: build-test:latest
```

</details>


### 이미지 히스토리 확인 명령어
- 해당 이미지가 어떤 단계(Dockerfile 명령어들)를 거쳐 만들어졌는지 빌드 이력을 확인
``` bash
docker history <image>
```


### 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `--no-trunc` | 생략된 빌드 명령을 잘림 없이 전체 출력한다. |

<details>
<summary>docker history 실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker history build-test
IMAGE          CREATED        CREATED BY                SIZE      COMMENT
e2ac70e7319a   4 months ago   CMD ["/hello"]            0B        buildkit.dockerfile.v0
<missing>      4 months ago   COPY hello / # buildkit   10.1kB    buildkit.dockerfile.v0
```
확인 가능 항목:
- 각 레이어가 생성될 때 실행된 명령어 (RUN, COPY, EXPOSE 등)
- 각 레이어가 차지하는 용량
- 이미지에 보안상 불필요한 레이어가 포함되어 있는지 확인할 때 유용합니다.

</details>


## 컨테이너 라이프사이클 관리
### 컨테이너 생성 및 실행 명령어
- 이미지를 기반으로 새로운 컨테이너를 생성하고 실행하는 명령어이다.
- 로컬에 이미지가 없으면 Docker Hub에서 이미지를 자동으로 다운로드(pull)한 후 컨테이너를 실행한다.

```bash
docker run [옵션] <image> [command]
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-d`, `--detach` | 백그라운드(Detached) 모드로 실행한다. |
| `-p`, `--publish` | 호스트와 컨테이너의 포트를 연결한다. (`<호스트 포트>:<컨테이너 포트>`) |
| `--name` | 컨테이너 이름을 지정한다. |
| `-v`, `--volume` | 호스트 디렉터리와 컨테이너 디렉터리를 마운트한다. |
| `-it` | 표준 입력을 유지하고 터미널을 연결한다. (`-i` + `-t`) |
| `--rm` | 컨테이너 종료 시 자동으로 삭제한다. |

<details>
<summary>docker run 실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/
```

</details>



### 컨테이너 목록 조회 명령어
- 현재 실행 중인 컨테이너 목록을 확인하는 명령어이다.

```bash 
docker ps
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-a`, `--all` | 종료된 컨테이너를 포함한 모든 컨테이너를 출력한다. |
| `-q`, `--quiet` | Container ID만 출력한다. |


<details>
<summary>docker ps 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
singainnn6931@c4r2s5 3_Docker % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
f6844b6b2a07   hello-world   "/hello"   5 seconds ago   Exited (0) 4 seconds ago             stoic_margulis
```
상태 분석
- CONTAINER ID: 컨테이너의 고유 식별자 (12자리 해시값)
- IMAGE: 컨테이너 생성에 사용된 베이스 이미지
- COMMAND: 컨테이너 시작 시 실행되는 프로세스/명령어
- CREATED: 컨테이너가 생성된 시점
- STATUS: 현재 컨테이너 상태 (Up, Exited, Created 등)
- PORTS: 포트 포워딩 설정 정보
- NAMES: 지정했거나 자동으로 생성된 컨테이너 이름

</details>

### 컨테이너 정지 명령어
- 실행 중인 컨테이너를 안전하게 종료하는 명령어이다.

``` bash
docker stop <container>
```

<details>
<summary>docker stop 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED         STATUS         PORTS     NAMES
77abf5b8836b   nginx     "/docker-entrypoint.…"   2 seconds ago   Up 2 seconds   80/tcp    zealous_northcutt

# 이름으로 정지
singainnn6931@c4r2s5 ~ % docker stop zealous_northcutt
zealous_northcutt

# Container ID로 정지
singainnn6931@c4r2s5 ~ % docker stop 77abf5b8836b
77abf5b8836b
```

</details>

### 컨테이너 재실행 명령어
- 정지된 컨테이너를 다시 시작하는 명령어이다.


``` bash
docker start <container>
```

<details>
<summary>docker start 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 ~ % docker start zealous_northcutt
zealous_northcutt

singainnn6931@c4r2s5 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED         STATUS         PORTS     NAMES
77abf5b8836b   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 9 seconds   80/tcp    zealous_northcutt
```

</details>

### 컨테이너 재시작 명령어
- 실행 중이거나 정지된 컨테이너를 다시 시작하는 명령어이다.

``` bash
docker restart <container>
```

``` bash
singainnn6931@c4r2s5 ~ % docker restart zealous_northcutt
zealous_northcutt

# 확인
singainnn6931@c4r2s5 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED         STATUS         PORTS     NAMES
77abf5b8836b   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 2 seconds   80/tcp    zealous_northcutt
```

### 컨테이너 삭제 명령어
- 더 이상 사용하지 않는 컨테이너를 삭제하는 명령어이다.
- 실행 중인 컨테이너는 먼저 `docker stop`으로 종료해야 한다.

``` bash
docker rm <container>
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-f`, `--force` | 실행 중인 컨테이너를 강제로 종료한 후 삭제한다. |
| `-v` | 컨테이너와 연결된 익명(Anonymous) 볼륨도 함께 삭제한다. |


<details>
<summary>docker rm 실행 결과</summary>

``` bash
# 컨테이너 정지 후 삭제
singainnn6931@c4r2s5 A_WebServer % docker stop my-web
my-web
singainnn6931@c4r2s5 A_WebServer % docker rm my-web
my-web

# 강제 삭제
singainnn6931@c4r2s5 ~ % docker rm zealous_northcutt
Error response from daemon: cannot remove container "zealous_northcutt": container is running: stop the container before removing or force remove
singainnn6931@c4r2s5 ~ % docker rm -f zealous_northcutt
zealous_northcutt
singainnn6931@c4r2s5 ~ % docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
singainnn6931@c4r2s5 ~ % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED          STATUS                      PORTS     NAMES

# 정지된 모든 컨테이너 일괄 삭제
singainnn6931@c4r2s5 A_WebServer % docker rm $(docker ps -a -q)
```

</details>

## 컨테이너 내부 접속 & 모니터링


### 컨테이너 내부 명령어 실행 (내부 접속)
- 실행 중인 컨테이너 내부에서 **새로운 프로세스(명령어)** 를 실행하는 명령어이다. 주로 Bash 또는 Sh 셸에 접속하거나 특정 명령을 실행할 때 사용한다.

``` bash
docker exec [옵션] <container> <command>
```

### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-i`, `--interactive` | 표준 입력(STDIN)을 유지하여 대화형 모드로 실행한다. |
| `-t`, `--tty` | 가상 터미널(TTY)을 할당한다. |
| `-u`, `--user` | 지정한 사용자 계정으로 명령을 실행한다. |


<details>
<summary>docker exec 실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker exec -it stoic_leakey bash
root@9d60981db75d:/# ls
bin   dev		   docker-entrypoint.sh  home  lib64  mnt  proc  run   srv  tmp  var
boot  docker-entrypoint.d  etc			 lib   media  opt  root  sbin  sys  usr
root@9d60981db75d:/# nginx -v
nginx version: nginx/1.31.3
```

</details>


### 실행 중인 컨테이너에 연결 (``)
- 실행 중인 컨테이너의 **메인 프로세스(Standard Input/Output)** 에 직접 연결하는 명령어이다.

```bash
docker attach <container>
```
`docker exec`와 달리 새로운 프로세스를 생성하지 않으며, 기존에 실행 중인 프로세스에 연결한다.

### 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `--detach-keys` | 컨테이너를 종료하지 않고 연결만 해제할 단축키를 지정한다. |



> **참고**
>
> - `docker exec` : 새로운 셸(또는 명령어)을 실행한다.
> - `docker attach` : 기존 메인 프로세스에 연결한다.
> - `Ctrl + P` → `Ctrl + Q`를 누르면 컨테이너를 종료하지 않고 연결만 해제할 수 있다.
> - `Ctrl + C`는 메인 프로세스에 전달되어 컨테이너가 종료될 수 있으므로 주의한다.



### 컨테이너 로그 조회 명령어
- 컨테이너의 메인 프로세스가 출력한 **표준 출력(STDOUT)** 및 **표준 오류(STDERR)** 로그를 확인하는 명령어이다.

``` bash
docker logs [옵션] <container>
```



### 옵션
| 옵션 | 설명 |
| :--- | :--- |
| `-f`, `--follow` | 로그를 실시간으로 출력한다. |
| `-t`, `--timestamps` | 로그와 함께 타임스탬프를 출력한다. |
| `--tail <n>` | 마지막 n개의 로그만 출력한다. |

<details>
<summary>실행 결과</summary>

![실행 당시 로그](<실행로그.png>)


``` bash
singainnn6931@c4r2s5 3_Docker % docker logs stoic_leakey 

/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/08/05 06:46:58 [notice] 1#1: using the "epoll" event method
2026/08/05 06:46:58 [notice] 1#1: nginx/1.31.3
2026/08/05 06:46:58 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/08/05 06:46:58 [notice] 1#1: OS: Linux 6.17.8-orbstack-00308-g8f9c941121b1
2026/08/05 06:46:58 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 20480:1048576
2026/08/05 06:46:58 [notice] 1#1: start worker processes
2026/08/05 06:46:58 [notice] 1#1: start worker process 29
2026/08/05 06:46:58 [notice] 1#1: start worker process 30
2026/08/05 06:46:58 [notice] 1#1: start worker process 31
2026/08/05 06:46:58 [notice] 1#1: start worker process 32
2026/08/05 06:46:58 [notice] 1#1: start worker process 33
2026/08/05 06:46:58 [notice] 1#1: start worker process 34
```

</details>

## 컨테이너 상태 & 모니터링


### 컨테이너/이미지 상세 정보 조회 명령어
- 컨테이너 또는 이미지의 설정 정보와 상태를 JSON 형식으로 출력하는 명령어이다.
- `-f` : Go 템플릿 문법을 사용하여 특정 키값만 추출 출력 (format)
- `--type` : 동일한 이름의 이미지와 컨테이너가 존재할 때 대상 유형 명시 (container 또는 image)

``` bash
docker inspect [옵션] <container|image>
```

### 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `-f`, `--format` | Go Template 문법을 사용하여 원하는 정보만 출력한다. |
| `--type` | 동일한 이름의 이미지와 컨테이너가 존재할 경우 조회 대상을 지정한다. (`container`, `image`) |



``` bash
singainnn6931@c4r2s5 3_Docker % docker inspect -f '{{.Id}}' stoic_leakey
9d60981db75d069f94974e5de7c805de5942811e7174de17382209689d58e47d
```

### 컨테이너 프로세스 조회 명령어
- 실행 중인 특정 컨테이너 내부에서 동작하고 있는 프로세스 목록을 확인
- 호스트 시스템에서 본 컨테이너 내부 프로세스의 PID와 실행 명령어를 확인 시 유용
``` bash
docker top <container>
```

<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 3_Docker % docker top stoic_leakey
PID                 USER                TIME                COMMAND
1600                root                0:00                nginx: master process nginx -g daemon off;
1630                dockrema            0:00                nginx: worker process
1631                dockrema            0:00                nginx: worker process
1632                dockrema            0:00                nginx: worker process
1633                dockrema            0:00                nginx: worker process
1634                dockrema            0:00                nginx: worker process
1635                dockrema            0:00                nginx: worker process
```
### 출력 항목

| 항목 | 설명 |
| :--- | :--- |
| `UID` | 프로세스를 실행한 사용자 |
| `PID` | 프로세스 ID |
| `PPID` | 부모 프로세스 ID |
| `CMD` | 실행 중인 프로세스(명령어) |

</details>

### 컨테이너 리소스 사용량 모니터링 명령어
- 실행 중인 컨테이너의 CPU, 메모리, 네트워크 I/O, 디스크 I/O 등의 리소스 사용량을 실시간으로 확인하는 명령어이다.
- `--no-stream` : 실시간 갱신 없이 실행 시점의 단일 결과만 출력 후 종료
- `-a` : 정지된 컨테이너까지 포함하여 리소스 현황 확인

``` bash
docker stats [옵션] [container...]
```

### 옵션

| 옵션 | 설명 |
| :--- | :--- |
| `--no-stream` | 현재 시점의 리소스 사용량만 출력하고 종료한다. |
| `-a`, `--all` | 실행 중인 컨테이너뿐만 아니라 정지된 컨테이너도 함께 표시한다. |


<details>
<summary>실행 결과</summary>

``` bash
singainnn6931@c4r2s5 ~ % docker stats --no-stream stoic_leakey 
CONTAINER ID   NAME           CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O        PIDS
9d60981db75d   stoic_leakey   0.00%     6.359MiB / 15.67GiB   0.04%     1.13kB / 126B   17.7MB / 4.1kB   7
```

</details>

## 볼륨 관리

### Docker 볼륨 생성 명령어
- 컨테이너와 독립적으로 데이터를 저장하기 위한 Docker 볼륨을 생성하는 명령어이다.

```bash
docker volume create <volume_name>
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker volume create my-volume
my-volume
```

</details>

### Docker 볼륨 목록 조회 명령어
- 현재 Docker에 생성되어 있는 볼륨 목록을 확인하는 명령어이다.

```bash
docker volume ls
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 ~ % docker volume ls
DRIVER    VOLUME NAME
local     my-volume
local     webserver-volume
```

### 출력 항목

| 항목 | 설명 |
| :--- | :--- |
| `DRIVER` | 볼륨 드라이버 종류 (기본값: `local`) |
| `VOLUME NAME` | 볼륨 이름 |


</details>


### Docker 볼륨 상세 정보 조회 명령어
- 특정 볼륨의 상세 정보를 JSON 형식으로 확인하는 명령어이다.

```bash
docker volume inspect <volume_name>
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 ~ % docker volume inspect my-volume
[
    {
        "CreatedAt": "2026-08-05T16:22:42+09:00",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/my-volume/_data",
        "Name": "my-volume",
        "Options": null,
        "Scope": "local"
    }
]
```

### 확인 가능한 항목

| 항목 | 설명 |
| :--- | :--- |
| `Name` | 볼륨 이름 |
| `Driver` | 사용 중인 볼륨 드라이버 |
| `Mountpoint` | 호스트에 실제 데이터가 저장되는 위치 |
| `Scope` | 볼륨의 적용 범위 |


</details>

### Docker 볼륨 삭제 명령어
- 더 이상 사용하지 않는 Docker 볼륨을 삭제하는 명령어이다.
- 사용 중인 볼륨은 삭제할 수 없으며, 먼저 해당 볼륨을 사용하는 컨테이너를 삭제하거나 분리해야 한다.

```bash
docker volume rm <volume_name>
```

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 3_Docker % docker volume rm my-volume
my-volume
```

</details>


## 네트워크

### Docker 네트워크 목록 조회 명령어
- Docker에 생성되어 있는 네트워크 목록을 확인하는 명령어이다.
- 기본적으로 Docker는 `bridge`, `host`, `none` 네트워크를 제공하며, 사용자가 직접 생성한 네트워크도 함께 표시된다.

```bash
docker network ls
```

### 기본 네트워크

| 네트워크 | 설명 |
| :--- | :--- |
| `bridge` | 기본 네트워크. 별도 설정이 없으면 컨테이너는 이 네트워크에 연결된다. |
| `host` | 호스트의 네트워크를 그대로 사용하는 방식이다. |
| `none` | 네트워크를 연결하지 않는다. |

<details>
<summary>실행 결과</summary>

```bash
singainnn6931@c4r2s5 ~ % docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
72f6bc24a3f2   bridge    bridge    local
bfd5f9b43483   host      host      local
06c4e2d2f040   none      null      local
```

### 출력 항목

| 항목 | 설명 |
| :--- | :--- |
| `NETWORK ID` | 네트워크의 고유 식별자 |
| `NAME` | 네트워크 이름 |
| `DRIVER` | 사용 중인 네트워크 드라이버 |
| `SCOPE` | 네트워크의 적용 범위 |

</details>
