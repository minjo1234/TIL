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

제가 담당한 인사 시스템은 휴가나 재택근무처럼 신청 타입이 다양했습니다. 그런데 문제는 공통으로 체크해야 하는 로직들이 각 서비스에 중복해서 들어가 있다 보니, 규정이 하나만 바뀌어도 관련된 모든 클래스를 일일이 찾아다니며 수정해야 했습니다. 단순히 수정이 번거로운 걸 넘어, 수정 과정에서 실수로 하나라도 누락하면 바로 장애로 이어지는 구조라 유지보수가 매우 불안정했습니다.

이를 해결하기 위해 로직을 기능별로 분리해서 순서대로 연결하는 책임 연쇄 패턴(Chain of Responsibility)을 도입했습니다. 각 기능을 독립된 단계로 나누고 Fluent API를 통해 필요한 순서대로 조합하게 만들었습니다. 덕분에 이제는 로직이 한 곳에서 관리되어 규정 변화에 훨씬 빠르고 안전하게 대응할 수 있게 되었습니다.


approval
approval_process : 결제 프로세스
approval_line_config  -> 결제라인
- approval_detail_config

1.휴저한명당, 해당 부서에 따라서 유저생성시 결제라인이 생성되도록 chain 을 설정해두었음.
