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

각각의 Controller, Service 등은 Chain 만 알면되고 다른 결제로직과의 의존성을 몰라도된다.
장점, 만약 회사의 결제 단계의 수정이 일어난다면 만약 승인단계가 변경된다면 
- 하나의 단계의 속하는 클래스만 Chain에서 제거해주면된다.
- ApiController는 Chain의 시작점의 역할을 
- 각각의 Chain들은 해당 클래스와의 의존관계가 없고 자신의 로직만 수행하고, 로직이 정상적으로 종료되면 다음 Chain 을 실행시킨다.




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


---

제가 담당한 인사 관리 시스템은 휴가, 재택, 유연 근무 등 다양한 신청 타입이 존재했습니다. 각 타입마다 공통적으로 거쳐야 하는 검증 로직이 있는 경우도 있지만, 특정 타입에만 필요한 로직(재택 시 장비 신청 등)도 있었습니다.

인사 시스템에서 회사 규정이 변경될경우 공통 로직을 이용하는 모든 서비스에서 해당 
이를 위해 Chain of Responsibility를 도입했고, 공통 핸들러와 전용 핸들러를 Fluent API로 유연하게 조합하여 코드 중복을 제거하고 비즈니스 변화에 유연하게 대응할 수 있도록 개선했습니다.