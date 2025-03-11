
### 1.mariadb 이미지 다운로드 

```docker
docker pull mariadb 
```

---
### 2.docker 컨테이너 실행

```docker 
docker run --name mariadb -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 mariadb 
```

---
### 3.컨테이너 접속

```docker
docker exec -it mariadb /bin/bash 
```

---
### 4.mariadb 접속

```sql
mariadb -u root -p 
```
----

