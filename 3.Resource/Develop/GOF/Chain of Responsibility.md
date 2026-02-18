책임 연쇄 패턴 

책임 분리(SRP) 원칙을 잘 따르는 패턴이다.
결제 로직이나 필터링 시스템에서 필수적이다.

Chain : 연결고리
Handler : 처리자

구성 ClassFile

Chain : nextChain, process method 구현체 존재
ChainHandlerFactory : Fluent(흐르는) API 설정, Chain 연결 
ChainHandler  : process method interface 


Qulifier 를 이용해서 하나의 Chain Bean 을 등록하낟.

각각의 Controller, Service 등은 Chain 만 알면되고 다른 결ㅈ





```





```java
@Getter
public class Chain {
	
	@Setter
	private Chain nextChain;
	private ChainHandler process ;
	
	public Chain(ChainHandler process){ this.process = process; }
	
	@Transactional(rollbackFor = Exception.class)  
	public <T> void process(T obj){  
	    this.process.process(obj);  
	    if(Objects.nonNull(this.nextChain)) this.nextChain.process(obj); 
	}
}
```


ChainHandler 
Chain 
	ChainHandlerFactory -> 


---


3. 일반적인 결재 로직 패턴 6가지
	- Chain of Responsibility (현재 적용)
	- State 패턴 (상태 관리)
	- Strategy 패턴 (승인 규칙)
	- Command 패턴 (작업 캡슐화)
	- Observer 패턴 (알림)
	- Template Method 패턴 (공통 로직)


| **구분**     | **NetApp (전통적 스토리지)**       | **Hadoop (빅데이터 프레임워크)**       |
| ---------- | --------------------------- | ----------------------------- |
| **정체성**    | 고성능 전용 스토리지 서버 (NAS/SAN)    | 일반 서버들을 묶어주는 소프트웨어            |
| **확장 방식**  | 장비 자체를 늘리거나 고사양화 (Scale-up) | 저렴한 컴퓨터를 계속 이어 붙임 (Scale-out) |
| **주요 목적**  | 데이터의 **빠르고 안정적인 저장 및 공유**   | 데이터의 **저장 + 대규모 병렬 분석**       |
| **데이터 형태** | 주로 정형 데이터 (문서, DB 파일 등)     | 비정형 데이터 (로그, 이미지, SNS 텍스트 등)  |
| **비용**     | 고가의 전용 장비와 라이선스 비용 발생       | 오픈소스 기반이라 하드웨어 구성비가 저렴함       |


휴가, 재택근무, 사용자 생성은 해당 Bean