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