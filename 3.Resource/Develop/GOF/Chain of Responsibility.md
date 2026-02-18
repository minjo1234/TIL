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

제가 담당한 인사 시스템은 휴가나 재택근무처럼 신청하는 종류가 아주 많았습니다. 그런데 문제는 회사 규정이 하나만 바뀌어도 이 서비스, 저 서비스에 흩어져 있는 코드들을 일일이 다 찾아가서 하나씩 고쳐줘야 했다는 점이었어요.

어디를 고쳐야 할지 찾는 것도 일이고, 혹시나 하나라도 빼먹고 안 고치면 바로 버그가 생기는 상황이라 유지보수가 너무 힘들었습니다.

그래서 이걸 해결하려고 로직을 레고 블록처럼 하나씩 쪼개서 관리하는 방식을 도입했습니다. 이제는 필요한 블록만 순서대로 끼워 맞추면(Chain) 되니까, 규정이 바뀌어도 한 곳만 수정하면 되고 새로운 신청 종류가 생겨도 금방 대응할 수 있게 되었습니다.