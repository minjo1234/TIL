Nginx has two functions 

- Web server 
- Reverse Proxy 

### Web server 

- define: A web server is a program that receives HTTP requests from clients (browsers) and responds with the necessary web data.”

---




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


## ✅ 이 설정의 핵심 포인트

✅ `events {}` : 기본 필수 블록  
✅ `http {}` : 메인 설정 블록  
✅ `log_format` : 기본 로그 형식  
✅ `server` : 각 도메인/백엔드 매핑  
✅ `proxy_pass` : 내부 `guacamole:8080` 으로 연결  
✅ `WebSocket` 헤더 : Guacamole은 **웹소켓 터널링** 필수라 반드시 필요!
