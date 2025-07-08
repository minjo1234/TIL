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

----

```
docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > initdb.sql
```

```
docker exec -it guac_db bash
mysql -u root -p guacamole_db < /initdb.sql
```

