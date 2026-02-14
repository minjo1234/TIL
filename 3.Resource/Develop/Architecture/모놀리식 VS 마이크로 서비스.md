### 1. 모놀리식 구조 (Monolithic Architecture)

- 모든 기능이 하나의 애플리케이션에 포함
- 단일 배포 단위
- 하나의 DB 

---
### 2. 마이크로서비스 구조 (Microservices Architecture)

사용 목적 : 
- 개발 속도 : 프로젝트 단위의 배포가 아닌, 서비스 단위의 배포가 가능하다.
- 기술 선택의 자유도 (Polyglot Architecture) : 실시간 채팅은 Node.js, 데이터 계산은 Python
	- Polyglot - 여러 언어를 구사한다.
- 장애 격리 (Fault Tolerance) : 하나의 서비스에서 장애가 통제된다.
- 스케일 아웃 (Selective Scaling, 대용량 트래픽) : 쿠폰 조회 기능만 사용량이 급증한다면, 쿠폰 서비스의 컨테이너 개수만 늘리면 된다.



- 각 기능을 독립적인 서비스로 분리
- 독립적인 배포 단위
- 각자 다른 데이터베이스



