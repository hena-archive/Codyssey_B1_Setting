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
