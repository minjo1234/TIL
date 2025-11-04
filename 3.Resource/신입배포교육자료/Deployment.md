
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
    ports:
	  - 8086:8086
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

---

docker-compose.yml (nginx o, nginx가 8086 포트를 이용하여 배포 한 경우)

```yml
services:
  nginx:
    image: clovirone_nginx
    container_name: clovirone_nginx
    ports:
      - "8086:8086"
    volumes:
      # logrotate 어디 위치시킬지 내일 고민해보자 쩝쩝 
      - nginx-logs:/var/log/nginx
      - ./nginx/logs-archive:/var/log/nginx-archive
      - ./nginx/conf.d/default.conf:/etc/nginx/conf.d/default.conf
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf
      - ./nginx/ssl:/etc/nginx/ssl
      - /usr/share/zoneinfo/Asia/Seoul:/etc/localtime:ro
    restart: unless-stopped
    networks:
      - net
    depends_on:
      - clovirone

  clovirone:
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
      - "gooddi-vcsa01.gooddi.lab:10.100.64.4"

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
  nginx-logs:
    driver: local

networks:
  net:
    driver: bridge
```


---


- 인사 DB/AD - query plugin (데이터 받아서 사내테스트 후 운영에 반영)





# 한 줄로 실행
docker exec db-container bash -c '
mysql -u clovirone -pClovirone3775* clovirone <<EOF
SELECT k.TABLE_NAME, k.COLUMN_NAME
FROM information_schema.KEY_COLUMN_USAGE k
WHERE k.TABLE_SCHEMA = "clovirone"
AND k.CONSTRAINT_NAME = "PRIMARY";
EOF
' | tail -n +2 | while read TABLE PK; do
  echo "Checking $TABLE.$PK..."
  docker exec db-container mysql -u clovirone -pClovirone3775* clovirone -e \
    "SELECT \`$PK\`, COUNT(*) as cnt FROM \`$TABLE\` GROUP BY \`$PK\` HAVING cnt > 1 LIMIT 5;" 2>/dev/null
done