
### 1.설정파일(properties) 수정

서버의 properties를 설정한다(IP, Port)

DB : domain-infra-product.xml 
	 (url, username, password)
	
WEB : webapp-product.properties 
	(server.port)

---
### 2.Docker File Build 

**web** 

```bash
# 프로젝트 루트 경로에서
docker build -t clovirone:latest
```

**nginx**

```bash
# 프로젝트 루트 경로에서
docker build -f  ocker-files/nginx/Nginx_Dockerfile -t clovirone_nginx:latest .               
```

 **db**
  
- ```
  # 프로젝트 루트 경로에서
  ```


### 3.Image to Tar 

---

**web** 

**nginx** 

**db** 


(domain-infra-product.xml)
(webapp-product.properties)

DB Connection 관련 password 설정 (JasyptKeyMakeTest.groovy)




DockerFile 
- web
- db 
- docker-compose.yml 





배포테스트 오늘 진행예정 

