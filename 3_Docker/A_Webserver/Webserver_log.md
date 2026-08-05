# 1. Docker 설치 및 기본 점검

Docker가 정상적으로 설치되어 있으며, Docker Engine(데몬)이 정상적으로 실행 중인지 확인하였다.

---

## 1.1 Docker 버전 확인

Docker CLI와 Docker Engine의 버전 정보를 확인하였다.

### 실행 명령

```bash
docker --version
docker version
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker --version
Docker version 28.5.2, build ecc6942

singainnn6931@c4r2s5 3_Docker % docker version

Client:
 Version:           28.5.2
 API version:       1.51
 Go version:        go1.25.3
 OS/Arch:           darwin/amd64
 Context:           orbstack

Server: Docker Engine - Community
 Engine:
  Version:          28.5.2
  API version:      1.51
  OS/Arch:          linux/amd64
```

### 결과 분석

- Docker CLI(Client)가 정상적으로 설치되어 있음을 확인하였다.
- Docker Engine(Server)이 정상적으로 실행 중임을 확인하였다.
- Client와 Server의 버전이 모두 **28.5.2**로 일치하여 정상적으로 통신하고 있음을 확인하였다.


## 1.2 Docker Engine 상태 확인

Docker Engine(데몬)의 실행 상태와 시스템 정보를 확인하였다.

### 실행 명령

```bash
docker info
```

### 실행 결과

```text
Server:
 Containers: 1
  Running: 1
  Stopped: 0
 Images: 2

 Server Version: 28.5.2

 Storage Driver: overlay2

 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64

 CPUs: 6
 Total Memory: 15.67GiB

 Docker Root Dir: /var/lib/docker
```

### 결과 분석

- Docker Engine(Server)이 정상적으로 실행 중임을 확인하였다.
- 현재 **1개의 컨테이너가 실행 중**이며, **2개의 Docker 이미지**가 저장되어 있음을 확인하였다.
- Storage Driver는 **overlay2**를 사용하고 있음을 확인하였다.
- Docker Engine은 **Linux 기반(OrbStack)** 환경에서 동작하고 있음을 확인하였다.
- Docker 데이터는 `/var/lib/docker` 경로에 저장됨을 확인하였다.


# 2. Docker 기본 운영 명령 수행

Docker 이미지와 컨테이너를 생성 및 관리하고, 로그와 리소스 사용량을 확인하여 Docker의 기본 운영 기능을 검증하였다.

## 2.1 이미지 다운로드 및 목록 확인

NGINX 이미지를 Docker Hub에서 다운로드한 후, 로컬 이미지 목록을 확인하였다.

### 실행 명령

```bash
docker pull nginx
docker images
```

### 실행 결과

```text
singainnn6931@c4r2s5 A_Webserver % docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
26c307b5e35a: Pull complete 
3c55dc422a81: Pull complete 
d84ae7b21412: Pull complete 
c0df8d325117: Pull complete 
b8b80b9bc028: Pull complete 
f5de6e85ac74: Pull complete 
5a4222b844e8: Pull complete 
Digest: sha256:640dee81b9ada2bf929ae17c2c7e88930f244216aa6418306226ce9bdc3271e6
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
```

```text
singainnn6931@c4r2s5 A_WebServer % docker images

singainnn6931@c4r2s5 A_Webserver % docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
nginx        latest    5253dc86cc93   9 hours ago   161MB
```


## 2.2 컨테이너 생성 및 실행

다운로드한 NGINX 이미지를 이용하여 컨테이너를 생성하고 실행하였다.

### 실행 명령

```bash
docker run -d --name my-web -p 8080:80 nginx
docker ps
docker ps -a
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker run -d --name my-web -p 8080:80 nginx
d14a4f23d6660a6219760f52cd48431b29f1943372a42009d4c67b998d24c301
```

```text
singainnn6931@c4r2s5 3_Docker % docker ps
CONTAINER ID   IMAGE     COMMAND                   CREATED         STATUS         PORTS                                     NAMES
d14a4f23d666   nginx     "/docker-entrypoint.…"   3 seconds ago   Up 2 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-web
```

### 결과 분석

- 컨테이너가 정상적으로 생성되어 실행되었다.
- `docker ps`를 통해 실행 중인 컨테이너를 확인하였다.
- `docker ps -a`를 통해 실행 중인 컨테이너와 종료된 컨테이너를 함께 확인할 수 있다.

---

## 2.3 컨테이너 로그 확인

실행 중인 컨테이너의 로그를 확인하였다.

### 실행 명령

```bash
docker logs my-web
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker logs my-web
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/08/05 09:29:14 [notice] 1#1: using the "epoll" event method
2026/08/05 09:29:14 [notice] 1#1: nginx/1.31.3
2026/08/05 09:29:14 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19) 
2026/08/05 09:29:14 [notice] 1#1: OS: Linux 6.17.8-orbstack-00308-g8f9c941121b1
2026/08/05 09:29:14 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 20480:1048576
2026/08/05 09:29:14 [notice] 1#1: start worker processes
2026/08/05 09:29:14 [notice] 1#1: start worker process 29
2026/08/05 09:29:14 [notice] 1#1: start worker process 30
2026/08/05 09:29:14 [notice] 1#1: start worker process 31
2026/08/05 09:29:14 [notice] 1#1: start worker process 32
2026/08/05 09:29:14 [notice] 1#1: start worker process 33
2026/08/05 09:29:14 [notice] 1#1: start worker process 34
```

## 2.4 컨테이너 리소스 사용량 확인

실행 중인 컨테이너의 CPU 및 메모리 사용량을 확인하였다.

### 실행 명령

```bash
docker stats --no-stream my-web
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker stats --no-stream my-web
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O         PIDS
d14a4f23d666   my-web    0.00%     5.934MiB / 15.67GiB   0.04%     1.13kB / 126B   16.3MB / 8.19kB   7
```

# 3. 컨테이너 실행 실습

Docker 컨테이너를 직접 실행하고 내부에 접속하여 기본 동작을 확인하였다. 또한 `exec`와 `attach` 명령을 비교하여 컨테이너와의 연결 방식 차이를 확인하였다.

## 3.1 hello-world 실행

Docker가 정상적으로 설치 및 동작하는지 확인하기 위해 `hello-world` 이미지를 실행하였다.

### 실행 명령

```bash
docker run hello-world
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:7f4da0fc94bcece205a8c0b6f4d11c8196924654ffe5c4d1aa439b7f632048b2
Status: Downloaded newer image for hello-world:latest

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

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```


## 3.2 Ubuntu 컨테이너 실행 및 내부 명령 수행

Ubuntu 이미지를 실행한 후 컨테이너 내부에 접속하여 간단한 Linux 명령을 실행하였다.

### 실행 명령

```bash
docker run -it ubuntu bash
```

### 실행 결과

```text
singainnn6931@c4r2s5 3_Docker % docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
617772c7d19b: Pull complete 
a7fb98a8eddd: Pull complete 
Digest: sha256:678c6550cc43645e08669028bc177f50be4e7c5b8cca677067b1914d4afc7a03
Status: Downloaded newer image for ubuntu:latest
```

컨테이너 내부에서 다음 명령을 실행하였다.

```bash
ls
echo hello
```

실행 결과

```bash
# bash에서 ls 실행
root@ef6d40df2fd6:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

# bash에서 echo hello 실행
root@ef6d40df2fd6:/# echo hello
hello
```

## 3.3 exec와 attach 비교

실행 중인 컨테이너에 접속하는 방법인 `docker exec`와 `docker attach`를 비교하였다.

### docker exec

```bash
docker exec -it my-web bash
```

#### 특징

- 실행 중인 컨테이너 내부에 **새로운 Bash 프로세스**를 생성하여 접속한다.
- `exit`로 셸을 종료해도 컨테이너는 계속 실행된다.
- 컨테이너 관리 및 디버깅 시 가장 많이 사용하는 방식이다.

---

### docker attach

```bash
docker attach my-web
```

#### 특징

- 실행 중인 컨테이너의 **메인 프로세스(PID 1)** 에 직접 연결한다.
- 메인 프로세스가 종료되면 컨테이너도 함께 종료된다.
- 웹 서버(NGINX)와 같이 터미널 입력을 받지 않는 프로그램은 화면 변화가 거의 없으며, 로그만 출력된다.

---

## exec와 attach 비교

| 항목 | docker exec | docker attach |
|------|-------------|---------------|
| 연결 대상 | 새로운 프로세스 생성 | 메인 프로세스(PID 1) |
| Bash 실행 | 가능 | 불가능(기존 프로세스에 연결) |
| `exit` 입력 | Bash만 종료 | 메인 프로세스 종료 시 컨테이너도 종료 |
| 주 용도 | 컨테이너 관리 및 디버깅 | 실행 중인 프로세스의 입출력 확인 |

### 결과 분석

실습을 통해 `docker exec`는 컨테이너 내부에 새로운 셸을 생성하여 안전하게 작업할 수 있는 반면, `docker attach`는 실행 중인 메인 프로세스와 직접 연결되는 방식임을 확인하였다. 따라서 일반적인 관리 및 디버깅 작업에서는 `docker exec`를 사용하는 것이 적합하다.

---

# 4. Dockerfile 기반 커스텀 이미지 제작

기존 웹 서버 이미지인 **NGINX**를 베이스 이미지로 사용하여 정적 웹 페이지와 웹 서버 설정을 변경한 커스텀 이미지를 제작하였다.

---

## 4.1 베이스 이미지 선택

이번 실습에서는 **NGINX 최신 공식 이미지(nginx:latest)** 를 베이스 이미지로 선택하였다.

### 선택 이유

- 공식적으로 제공되는 안정적인 웹 서버 이미지이다.
- 정적 웹 페이지를 쉽게 서비스할 수 있다.
- Dockerfile을 이용하여 HTML과 NGINX 설정만 변경하면 쉽게 커스터마이징할 수 있다.

---

## 4.2 프로젝트 구조

```text
A_WebServer
├── Dockerfile
├── nginx.conf
└── html
    └── index.html
```

![구조](<스크린샷 2026-08-05 오후 6.42.42.png>)

---

## 4.3 Dockerfile

```Dockerfile
# FROM : Docker 이미지를 만들 때 기반(Base) 이미지를 지정하는 명령
FROM nginx:latest

# 파일 복사
COPY nginx.conf /etc/nginx/nginx.conf

# 파일 복사
COPY html/index.html /usr/share/nginx/html/index.html

# 포트를 열어주는 명령어가 아님 그냥 기록 느낌
EXPOSE 2345

# 컨테이너가 시작될 때 실행할 기본 명령을 지정
# CMD ["nginx", "-g", "daemon off;"]
```

### 적용한 커스텀 포인트

| 적용 내용 | 목적 |
|-----------|------|
| nginx:latest 사용 | NGINX 웹 서버 기반 이미지 사용 |
| nginx.conf 교체 | 웹 서버 설정 변경 |
| index.html 교체 | 기본 페이지 대신 사용자 정의 페이지 제공 |

---

## 4.4 이미지 빌드

### 실행 명령

```bash
docker build -t webserver-image .
```

### 실행 결과

```bash
singainnn6931@c4r2s5 A_Webserver % docker build -t webserver-image .
[+] Building 0.5s (8/8) FINISHED                                                 docker:orbstack
 => [internal] load build definition from Dockerfile                                        0.1s
 => => transferring dockerfile: 451B                                                        0.0s
 => [internal] load metadata for docker.io/library/nginx:latest                             0.0s
 => [internal] load .dockerignore                                                           0.1s
 => => transferring context: 2B                                                             0.0s
 => [1/3] FROM docker.io/library/nginx:latest                                               0.0s
 => [internal] load build context                                                           0.1s
 => => transferring context: 91B                                                            0.0s
 => CACHED [2/3] COPY nginx.conf /etc/nginx/nginx.conf                                      0.0s
 => CACHED [3/3] COPY html/index.html /usr/share/nginx/html/index.html                      0.0s
 => exporting to image                                                                      0.0s
 => => exporting layers                                                                     0.0s
 => => writing image sha256:8ffd0d2776a72c5432aefe535a94f45ac514d2f00771fee2a6be4cb53980ce  0.0s
 => => naming to docker.io/library/webserver-image                                          0.0s
```



```bash
docker images
```

실행 결과

```bash
singainnn6931@c4r2s5 A_Webserver % docker images
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
webserver-image   latest    8ffd0d2776a7   43 seconds ago   161MB
nginx             latest    5253dc86cc93   9 hours ago      161MB
ubuntu            latest    86a1a31fdd84   11 days ago      100MB
hello-world       latest    e2ac70e7319a   4 months ago     10.1kB
```

---

## 4.5 컨테이너 실행

### 실행 명령

```bash
docker run -d --name webserver -p 8088:80 -v webserver-volume:/usr/share/nginx/html webserver-image
```

### 실행 결과

```bash
docker ps
```

실행 결과

```bash
docker run -d --name webserver -p 8088:80 -v webserver-volume:/usr/share/nginx/html webserver-image
112fcd42f081d57b4630245c96b7181976f3486e085c8e6402d5c97800693258


CONTAINER ID   IMAGE             COMMAND                   CREATED          STATUS          PORTS                                               NAMES
112fcd42f081   webserver-image   "/docker-entrypoint.…"   17 seconds ago   Up 17 seconds   2345/tcp, 0.0.0.0:8088->80/tcp, [::]:8088->80/tcp   webserver
d14a4f23d666   nginx             "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp             my-web
```

### 결과 분석

- 컨테이너가 정상적으로 실행되었다.
- 호스트의 **8088 포트**가 컨테이너 **80 포트**와 연결되었다.
- Named Volume이 정상적으로 연결되었다.

---

## 4.6 웹 서비스 접속 확인

웹 브라우저와 curl 명령을 이용하여 정상적으로 서비스되는 것을 확인하였다.

### 실행 명령

```bash
curl http://localhost:8088
```

### 실행 결과

```bash
singainnn6931@c4r2s5 A_Webserver % curl http://localhost:8088
<h1>Bind Mount Test</h1>
```

### 결과 분석

NGINX가 정상적으로 실행되며 Dockerfile에서 적용한 index.html이 정상적으로 서비스되는 것을 확인하였다.

![실행 화면](<스크린샷 2026-08-05 오후 6.48.15.png>)


# 5. Bind Mount 적용 확인

Bind Mount를 이용하여 호스트에서 수정한 파일이 컨테이너에 즉시 반영되는지 확인하였다.

---

## 5.1 Bind Mount 실행

### 실행 명령

```bash
singainnn6931@c4r2s5 A_Webserver % docker run -d --name bind-web -p 9000:80 -v ./html:/usr/share/nginx/html nginx
3e068b3a89add9132b91f277ff66d9989b60032299eafc5f851a62c89362c94d
```

---

## 5.2 변경 전 확인

```bash
curl http://localhost:9000
```

실행 결과
```bash
singainnn6931@c4r2s5 A_Webserver % curl http://localhost:9000
```
```html

<!DOCTYPE html>
<html>
<head>
    <title>Docker Persistence</title>
</head>
<body>
    <h1>Custom NGINX Server</h1>

    <h2>Docker Image + Volume Persistence</h2>

    <p>This page is served from a custom Docker image.</p>

    <p>
        When this folder is mounted as a Docker Volume,
        changes remain even after deleting the container.
    </p>
</body>
</html>
```

📷 **변경 전 브라우저 화면 첨부**
![변경 전](<스크린샷 2026-08-05 오후 7.02.20.png>)
---

## 5.3 호스트 파일 수정

호스트의 `html/index.html` 파일을 수정하였다.

변경 전

---

## 5.4 변경 후 확인

```bash
curl http://localhost:9000
```

실행 결과

![변경 후](<스크린샷 2026-08-05 오후 7.02.58.png>)

### 결과 분석

호스트에서 수정한 HTML 파일이 컨테이너를 다시 생성하지 않아도 즉시 반영되는 것을 확인하였다.

이는 Bind Mount가 호스트 디렉터리와 컨테이너 디렉터리를 직접 연결하기 때문이다.

📷 **변경 후 브라우저 화면 첨부**
