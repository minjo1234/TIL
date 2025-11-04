
### 1.설정파일(properties) 수정
---

서버의 properties를 설정한다(IP, Port)

DB : domain-infra-product.xml 
	 (url, username, password)
	
WEB : webapp-product.properties 
	(server.port)

### 2.Docker File Build 
---

**web** 

```bash
# 프로젝트 루트 경로에서
docker build -t clovirone:latest
```

**nginx**

```bash

docker build -f  docker-files/nginx/Nginx_Dockerfile -t clovirone_nginx:latest .               
```

 **db**

```bash
# 프로젝트 루트 경로에서
ocker build -f docker-files/db/DB_Dockerfile -t clovirone_db:latest .
```

### 3.Image to Tar 
---

**web** 

```bash
docker save -o clovirone.tar clovirone:latest
```

**nginx** 

```
docker save -o clovirone_nginx.tar clovirone_nginx:latest
```

**db** 

```bash
docker save -o clovirone_db.tar clovirone_db:latest
```

### 4.docker-compose.yml 
---

docker-compose.yml (nginx X)

```yml
services:
  web:
    image: clovirone
    container_name: clovirone
    volumes:
      - logs:/opt/tomcat/logs
      - backups:/opt/tomcat/backups
      - /usr/share/zoneinfo/Asia/Seoul:/etc/localtime:ro
    environment:
      - JAVA_OPTS=-Dspring.profiles.active=production -Duser.language=ko -Duser.country=KR -Dfile.encoding=UTF-8
      - JAVA_TOOL_OPTIONS=-Dsaaj.use.cache=false
      - CATALINA_OPTS=-Dspring.profiles.active=production -Duser.language=ko -Duser.country=KR -Dfile.encoding=UTF-8
      - JASYPT_PWD=${JASYPT_PWD:-$(cat ./jasypt_pwd.txt)}
    restart: unless-stopped
    networks:
      - net
    security_opt:
      - no-new-privileges:true
    depends_on:
      - db
    extra_hosts:
      - "domain:ip"
  db:
    image: clovirone_db
    container_name: clovirone_db
    volumes:
      - ./db/my.cnf:/etc/mysql/my.cnf:rw
      - db_data:/var/lib/mysql
      - /usr/share/zoneinfo/Asia/Seoul:/etc/localtime:ro
    restart: unless-stopped
    networks:
      - net

volumes:
  logs:
    driver: local
  backups:
    driver: local
  db_data:
    driver: local

networks:
  net:
    driver: bridge
```



db folder, db volume, serverTime 동기화 
docker-compose.yml (nginxr가 포함된 경우)





DB Connection 관련 password 설정 (JasyptKeyMakeTest.groovy)






1. <p align="left"></p>