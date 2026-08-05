# 내 컴퓨터에 개발자용 '작업실' 꾸미기

### 프로젝트 개요
Terminal, Docker, Git을 이용해 개발 환경을 직접 구축하고, 각 과정과 실행 결과를 기록하여 재현 가능한 개발 워크스테이션을 만드는 것을 목표로 한다.

### 실행 환경
| 항목 | 확인 명령어 |내용 |
|------|------|------|
| OS | `sw_vers` | macOS 15.7.4 |
| Shell | `echo $SHELL` | zsh |
| Terminal | `echo $TERM_PROGRAM` | Apple_Terminal |
| Docker 버전 | `docker --version` | Docker version 28.5.2 |
| Git 버전 | `git --version` | git version 2.53.0 |

### 수행 체크리스트
- [x] [터미널 기본 조작](1_Terminal/Terminal_Command.md)
- [x] [권한](2_Permission/Permission.md)
- [x] [Docker](3_Docker/Docker_Command.md)
  - [x] [사용중인 Dockerfile](3_Docker/A_Webserver/Dockerfile)
  - [x] [Dockerfile](3_Docker/A_Webserver/Dockerfile_cmd.md)
  - [x] [포트]()
  - [x] [볼륨]() 
- [x] [Git과 Github](4_Git/git_config.md)


### 트러블 슈팅
- [권한 에러](2_Permission/Error.md)
