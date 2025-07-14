reference document  
>  https://guacamole.apache.org/doc/gug/guacamole-docker.html


### Guecamole docker 

| Container                      | Role                                     | 예시 이미지                       |
| ------------------------------ | ---------------------------------------- | ---------------------------- |
| 1️⃣ `guacd` (Guacamole Daemon) | SSH/RDP/VNC  Connection process daemon   | `guacamole/guacd`            |
| 2️⃣ `guacamole` (Webapp)       | HTML5 + REST API Server                  | `guacamole/guacamole`        |
| 3️⃣ `DB` (MySQL or PostgreSQL) | User account, Connection Info, Authority | `mysql:5.7` or `postgres:13` |

---



`-v`: 모든 named volume 포함 삭제 (`db-data` 포함)

`entrypoint  : It must be executed when starting the container 

---

### Docker volume vs Mount point 

`Docker Volume`

- Docker management independent storage 
- backup, restoration, share goood


