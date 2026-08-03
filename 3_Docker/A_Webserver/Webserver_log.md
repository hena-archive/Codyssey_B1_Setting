# 1. 이미지 빌드
``` bash
docker build [OPTIONS] -t [IMAGE_NAME]:[TAG] [PATH | URL | -]
```


### 구성 요소

| 항목 | 설명 |
|------|------|
| `[옵션]` | 이미지 빌드 시 사용할 추가 옵션입니다. (예: `--no-cache`, `-f` 등) |
| `-t` | 생성할 이미지의 이름과 태그(Tag)를 지정하는 옵션입니다. |
| `[이미지 이름]` | 생성할 Docker 이미지의 이름입니다. |
| `[태그]` | 이미지의 버전을 의미하며, 생략하면 `latest`가 기본값으로 사용됩니다. |
| `[Dockerfile 경로(빌드 컨텍스트)]` | Dockerfile과 빌드에 필요한 파일들이 위치한 디렉터리입니다. 일반적으로 현재 디렉터리를 의미하는 `.`을 사용합니다. |


``` bash
singainnn6931@c4r2s5 A_Webserver % docker build -t webserver-image .
[+] Building 1.2s (8/8) FINISHED                                docker:orbstack
 => [internal] load build definition from Dockerfile                       0.1s
 => => transferring dockerfile: 449B                                       0.0s
 => [internal] load metadata for docker.io/library/nginx:latest            0.0s
 => [internal] load .dockerignore                                          0.1s
 => => transferring context: 2B                                            0.0s
 => [internal] load build context                                          0.1s
 => => transferring context: 855B                                          0.0s
 => CACHED [1/3] FROM docker.io/library/nginx:latest                       0.0s
 => [2/3] COPY nginx.conf /etc/nginx/nginx.conf                            0.1s
 => [3/3] COPY html/index.html /usr/share/nginx/html/index.html            0.2s
 => exporting to image                                                     0.3s
 => => exporting layers                                                    0.2s
 => => writing image sha256:0f087d9ff2d5a53385949bf65c2424b1825045f92d698  0.0s
 => => naming to docker.io/library/webserver-image                         0.0s

# 이미지 생성 확인
singainnn6931@c4r2s5 A_Webserver % docker images
REPOSITORY        TAG       IMAGE ID       CREATED         SIZE
webserver-image   latest    0f087d9ff2d5   5 minutes ago   161MB
nginx             latest    4e5db4761e0f   2 weeks ago     161MB
```

# 2. 볼륨 생성
```bash
docker volume create [옵션] [Volume 이름]
```

### 구성 요소

| 항목 | 설명 |
|------|------|
| `[옵션]` | Volume 생성 시 사용할 추가 옵션입니다. (예: `--driver`, `--label` 등) |
| `[Volume 이름]` | 생성할 Docker Volume의 이름입니다. 동일한 이름의 Volume이 이미 존재하면 기존 Volume을 사용합니다. |

### 예시

```bash
docker volume create webserver-volume
```

``` bash
singainnn6931@c4r2s5 1_Setting % docker volume create webserver-volume
webserver-volume
singainnn6931@c4r2s5 1_Setting % docker volume ls
DRIVER    VOLUME NAME
local     webserver-volume
```


# 3. 컨테이너 실행
``` bash
singainnn6931@c4r2s5 1_Setting % docker run -d --name webserver -p 8088:80 -v webserver-volume:/usr/share/nginx/html webserver-image
d7f93c1f8742ef81c18009ee9ad73721c7c705a249aab294da1e382270768dcf
singainnn6931@c4r2s5 1_Setting % docker ps
CONTAINER ID   IMAGE             COMMAND                   CREATED         STATUS          PORTS                                     NAMES
d7f93c1f8742   webserver-image   "/docker-entrypoint.…"   9 seconds ago   Up 10 seconds   0.0.0.0:8088->80/tcp, [::]:8088->80/tcp   webserver
```

## 컨테이너 실행 (Volume 마운트)

생성한 Docker 이미지를 기반으로 컨테이너를 실행하고, **Named Volume**을 마운트하여 웹 콘텐츠의 영속성을 확인합니다.

### 실행 명령어

```bash
docker run -d --name webserver -p 8088:80 -v webserver-volume:/usr/share/nginx/html webserver-image
```

### 구성 요소

| 항목 | 설명 |
|------|------|
| `docker run` | Docker 이미지를 기반으로 새로운 컨테이너를 생성하고 실행합니다. |
| `-d` | 컨테이너를 백그라운드(Detached Mode)에서 실행합니다. |
| `--name webserver` | 컨테이너의 이름을 `webserver`로 지정합니다. |
| `-p 8088:80` | 호스트(macOS)의 **8088번 포트**를 컨테이너의 **80번 포트**와 연결합니다. |
| `-v webserver-volume:/usr/share/nginx/html` | `webserver-volume`이라는 **Named Volume**을 컨테이너의 `/usr/share/nginx/html` 디렉터리에 마운트합니다. |
| `webserver-image` | 실행할 Docker 이미지의 이름입니다. |

### 실행 결과 확인

```bash
docker ps
```

예시 출력

```text
CONTAINER ID   IMAGE             COMMAND                   STATUS         PORTS                                     NAMES
d7f93c1f8742   webserver-image   "/docker-entrypoint.…"   Up 10 seconds  0.0.0.0:8088->80/tcp, [::]:8088->80/tcp   webserver
```

### 실행 결과 설명

- `STATUS`가 **Up**이면 컨테이너가 정상적으로 실행 중인 상태입니다.
- `PORTS`의 `8088->80`은 호스트의 **8088번 포트**가 컨테이너의 **80번 포트**와 연결되었음을 의미합니다.
- `NAMES`에는 지정한 컨테이너 이름인 `webserver`가 표시됩니다.

### Volume 마운트 구조

```text
Docker Engine
│
├── webserver (Container)
│      │
│      └── /usr/share/nginx/html
│                │
│                ▼
└── webserver-volume (Named Volume)
```

컨테이너의 `/usr/share/nginx/html` 디렉터리는 `webserver-volume`과 연결되어 있습니다. 따라서 해당 경로에 생성하거나 수정한 파일은 컨테이너가 아닌 **Named Volume**에 저장됩니다.

### Volume 연결 확인

```bash
docker inspect webserver
```

출력 결과의 `Mounts` 항목에서 다음과 같이 확인할 수 있습니다.

```json
"Mounts": [
  {
    "Type": "volume",
    "Name": "webserver-volume",
    "Destination": "/usr/share/nginx/html"
  }
]
```

이는 `webserver` 컨테이너가 `webserver-volume`을 `/usr/share/nginx/html`에 정상적으로 마운트하여 사용하고 있음을 의미합니다.



## Volume과 Bind Mount 비교

| 항목 | Volume | Bind Mount |
|------|--------|------------|
| **저장 위치** | Docker가 관리하는 저장소 | 호스트(macOS)의 지정한 폴더 |
| **호스트에서 직접 확인** | macOS에서는 직접 확인 불가능 | 가능 (`ls`, `cat`, Finder 등) |
| **Docker가 관리** | O | X |
| **주 용도** | 데이터 영속성(Persistence), 운영 환경 | 개발 환경, 파일 공유 |