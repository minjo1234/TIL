Nginx has two functions 

- Web server 
- Reverse Proxy 

### Web server 

- define: A web server is a program that receives HTTP requests from clients (browsers) and responds with the necessary web data.”

---

### 1.defind nginx.conf file 

```
# nginx.conf

events {}

http {
    # 기본 로그 형식
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';

    access_log /var/log/nginx/access.log main;
    error_log /var/log/nginx/error.log warn;

    # Guacamole 리버스 프록시
    server {
        listen 80;
        server_name guacamole.example.com;

        location / {
            proxy_pass http://10.200.1.120:8080/guacamole/;
            # proxy_pass http://127.0.0.1:8080/guacamole/;


            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;

            # WebSocket 지원 (Guacamole 필수)
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
    }

    # 필요하면 여기 아래에 다른 서비스 프록시도 추가 가능!
    # 예)
    #
    # server {
    #     listen 80;
    #     server_name jenkins.example.com;
    #
    #     location / {
    #         proxy_pass http://jenkins:8080/;
    #         proxy_set_header Host $host;
    #         proxy_set_header X-Real-IP $remote_addr;
    #     }
    # }
}
```

## ✅ 이 설정의 핵심 포인트

✅ `events {}` : 기본 필수 블록  
✅ `http {}` : 메인 설정 블록  
✅ `log_format` : 기본 로그 형식  
✅ `server` : 각 도메인/백엔드 매핑  
✅ `proxy_pass` : 내부 `guacamole:8080` 으로 연결  
✅ `WebSocket` 헤더 : Guacamole은 **웹소켓 터널링** 필수라 반드시 필요!

---

### 2.docker run 

```bash
docker run -d   --name nginx-proxy   -p 80:80   -v ~/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro   nginx:alpine

```

---

### Reverse Proxy 

#### 1.Client -> Reverse Proxy 
#### 2.Reverse Proxy -> Backend (Application Server)
#### 3.Back end -> Reverse Proxy 
#### 4. Reverse Proxy -> Clients

---

[Browser] 
  ↓
[Docker Nginx] :80 (컨테이너)
  ↓
[Guacamole] :8080 (컨테이너)

----

외부에서 접속하는 호스트는 알아야한다.
> **“이 도메인 이름을 어느 IP로 보내줄까?”만 결정**


- **포트 번호는 hosts랑 아무 상관 없음!**
- 포트는 `브라우저 요청`이나 `Nginx 설정`에서 따로 결정됨.