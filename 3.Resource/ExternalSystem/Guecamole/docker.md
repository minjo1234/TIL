reference document  
>  https://guacamole.apache.org/doc/gug/guacamole-docker.html



### Guecamole docker 

| Container                      | Role                                     | 예시 이미지                       |
| ------------------------------ | ---------------------------------------- | ---------------------------- |
| 1️⃣ `guacd` (Guacamole Daemon) | SSH/RDP/VNC  Connection process daemon   | `guacamole/guacd`            |
| 2️⃣ `guacamole` (Webapp)       | HTML5 + REST API Server                  | `guacamole/guacamole`        |
| 3️⃣ `DB` (MySQL or PostgreSQL) | User account, Connection Info, Authority | `mysql:5.7` or `postgres:13` |
|                                |                                          |                              |
|                                |                                          |                              |


---
**“Nginx가 IP → 도메인으로 바꿔주는 역할은 뭐라고 부르냐?”**
## 📌 정답:
Nginx가 하는 역할의 정확한 이름은 **리버스 프록시 (Reverse Proxy)** 입니다.

