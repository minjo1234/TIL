### 1.서버접속

---

### **2️⃣ Docker 네트워크 생성**

`docker network create <network-name>` 

✔️ Example:

`docker network create guac-net` 

---

### 3️⃣ Guacamole Daemon(guacd) 배포

`docker run -d \   --name guacd \   --network <network-name> \   guacamole/guacd`

---

### 3️⃣ MySQL (Guacamole DB) 실행

`docker volume create guac-db-data  # 최초 1회 initdb.sql 파일등록  mkdir -p <init 디렉토리 경로> ex) mkdir -p /clovirone2.0/volumes/guacamole/init  # docker container 실행   docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > <initdb.sql> 파일 경로 ex) docker run --rm guacamole/guacamole /opt/guacamole/bin/initdb.sh --mysql > /clovirone2.0/volumes/guacamole/init/initdb.sql  # MySQL 컨테이너 실행 docker run -d \   --name guac-db \   --network clovirone_network \   -e MYSQL_ROOT_PASSWORD=rootpass \   -e MYSQL_DATABASE=guacamole_db \   -e MYSQL_USER=guacuser \   -e MYSQL_PASSWORD=guacpass \   -v guac-db-data:/var/lib/mysql \   -v /clovirone2.0/volumes/guacamole/init/initdb.sql:/docker-entrypoint-initdb.d/initdb.sql \   mysql:8 \   --default-authentication-plugin=mysql_native_password`

---

#### 4️⃣ Guacamole Web 실행 (DB 인증 기반)

`docker run -d \   --name guacamole \   --network clovirone_network \   -e GUACD_HOSTNAME=guacd \   -e MYSQL_HOSTNAME=guac-db \   -e MYSQL_DATABASE=guacamole_db \   -e MYSQL_USER=guacuser \   -e MYSQL_PASSWORD=guacpass \   -p 8080:8080 \   guacamole/guacamole`

---
