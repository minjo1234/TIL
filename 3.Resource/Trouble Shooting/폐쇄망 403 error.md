
[2025.09.29 00:44:00.111] [http-nio-8888-exec-10] | -WARN  1 --- o.s.w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.web.bind.MissingServletRequestParameterException: Required request parameter 'systemId' for method parameter type Long is present but converted to null] 

menuStauts

---

- docker-files folder upload 

```bash
docker build -t clovirone:latest --no-cache --platform linux/amd64 .
```

docker build 를 제대로 했는데 이상한 컬럼을 조회하는 에러가 발생했음

![[Pasted image 20250929131022.png]]


[2025.09.29 05:08:29.295] [http-nio-8888-exec-1] | -WARN  1 --- o.s.w.s.m.s.DefaultHandlerExceptionResolver : Resolved [org.springframework.web.bind.MissingServletRequestParameterException: Required request parameter 'systemId' for method parameter type Long is present but converted to null] 

---

### Trouble Shooting 

상황 : 인천국제공항공사에서 외부시스템 등록이라는 메뉴를 사용하는 도중에 connectionTest 하는 부분에서 403 error가 발생했다. 

해결책 : 
- 서비스는 Jwt 인증방식을 사용하고 있기때문에 
CM-TOKEN, JSESSIONID 값이 정상적으로 되어있는지 확인하였고 이 부분에서는 문제가 존재하지 않았다.

그리하여 
사내데모 서버에서 403 error가 아닌 정상적으로 기능이 작동하는 container image를  tar로 제작하여, 오류가 있는 서버에 재배포하기로 하였다.

- volume, network 등 세팅을 모두 제거하였고 재배포하였지만 정상적으로 작동하는 이미지마저도 해당 서버에서는 에러가 발생하였다. 

이를 해결하기 위해 

- 이미지 명은 항상 동일하였기 때문에 이미지 명을 수정해보기로 마음을 먹었다. 
	- clovirone:latest -> test:latest 
	  > docker image tag clovirone:latest test:latest 


**하지만 에러가 발생하는 서버에서는 해당 에러가 발생하였다 .**

Caused by: java.lang.ExceptionInInitializerError: Exception java.lang.Error: javax.xml.soap.SOAPException: Unable to create SAAJ meta-factory: Error while searching for service [javax.xml.soap.SAAJMetaFactory] [in thread "scheduling-1"]

이와 같은 에러가 발생하는 이유는 

- JDK 버전의 차이 (Java 11 이상부터는 SOAP, JAX-WS 모듈이 JDK에 포함되지 않는다)
  > 오류가 발생하는, 발생하지 않는 서버가 모두 같은 JDK 버전을 사용하고 있기 때문에 무방하다.

- 컨테이너 환경의 차이 (호스트 OS)
  > Ubuntu 20.0.4.2 vs Ubuntu 24.4.2 를 사용하는 차이가 존재한다.

-  **서비스 로더(Service Provider) 메커니즘 문제**
>  이 부분이 가장 유력해 보였는데 그 이유는 초반에 Cashing으로 읽지 못하는 경우가 있었다 그래서 캐시 크기를 조정해보려고한다.

먼저 docker exec <container-name> bash 로 접근 후 

>  ls -l /opt/tomcat/webapps/ROOT/WEB-INF/lib/ | grep saaj  

해당 명령어에 읽기 권한이 있는지 체크를 한다. 
이때 SAAJ 구현체란 ?  

- **SAAJ** = _SOAP with Attachments API for Java
  (SOAP 메시지를 자바에서 만들고 처리하기 위한 표준 API)

이제 no-cache option을 추가한 후 재기동을 하려고한다.

docker compose down -v
docker system prune -af (캐시 레이어, 중지 컨테이너, 사용되지 않는 네트워크, 모든 unused 이미지 -a 옵션으로 지우기)
docker volume prune -f
docker compose up -d --build

- OS 보안취약점 확인해봐야할듯
