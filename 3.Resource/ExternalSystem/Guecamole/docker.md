reference document  
>  https://guacamole.apache.org/doc/gug/guacamole-docker.html



### Guecamole docker 

| Container                      |                                                            | 예시 이미지                       |
| ------------------------------ | ---------------------------------------------------------- | ---------------------------- |
| 1️⃣ `guacd` (Guacamole Daemon) | 실제 SSH/RDP/VNC 연결 처리 데몬. 사용자의 요청을 받아서 대상 서버에 연결하고, 화면을 전달. | `guacamole/guacd`            |
| 2️⃣ `guacamole` (Webapp)       | 사용자가 접속하는 HTML5 웹 클라이언트 + REST API 서버.                     | `guacamole/guacamole`        |
| 3️⃣ `DB` (MySQL or PostgreSQL) | 사용자 계정, 연결 정보(Connection), 권한 같은 설정 정보 저장.                 | `mysql:5.7` or `postgres:13` |




