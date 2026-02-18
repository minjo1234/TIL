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

---

좋은 질문입니다! approvalLineConfigId가 어디서 오는지 전체 흐름을 추적해보겠습니다.                                                                                                                      
                                                                                                                                                                                                           
⏺ Searched for 1 pattern, read 1 file (ctrl+o to expand)                                                                                                                                                   
  ⎿  PreToolUse:Grep says: Hookify import error: No module named 'hookify'                                                                                                                                 
  ⎿  PostToolUse:Grep says: Hookify import error: No module named 'hookify'                                                                                                                                
  ⎿  PreToolUse:Read says: Hookify import error: No module named 'hookify'
  ⎿  PostToolUse:Read says: Hookify import error: No module named 'hookify'                                                                                                                                
   
⏺ 완벽합니다! 이제 전체 흐름이 명확해졌습니다. approvalLineConfigId가 어디서 오는지 단계별로 설명하겠습니다.                                                                                               
                                 
⏺ Searched for 2 patterns (ctrl+o to expand)                                                                                                                                                               
  ⎿  PreToolUse:Glob says: Hookify import error: No module named 'hookify'
  ⎿  PostToolUse:Glob says: Hookify import error: No module named 'hookify'                                                                                                                                
  ⎿  PreToolUse:Grep says: Hookify import error: No module named 'hookify'
  ⎿  PostToolUse:Grep says: Hookify import error: No module named 'hookify'                                                                                                                                
                                 
⏺ 완벽합니다! 이제 전체 흐름이 명확해졌습니다. 화면에서부터 DB까지 approvalLineConfigId가 어떻게 전달되는지 상세하게 설명하겠습니다.                                                                       
                                                                                                                                                                                                           
  📊 approvalLineConfigId 데이터 플로우                                                                                                                                                                    
                                 
  전체 흐름 다이어그램                                                                                                                                                                                     
                                 
  ┌─────────────────────────────────────────────────────────────┐
  │ 1️⃣화면 로딩 (vacation_info.html)                            │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      GET /api/approval/getLineConfigByRequesterId
                          ↓
      DB 조회: approval_line_config (사용자별 결재선 목록)
                          ↓
      Response: [
          {id: 5, title: "일반 결재선", lineType: "DEFAULT"},
          {id: 6, title: "긴급 결재선", lineType: "CUSTOM"}
      ]
                          ↓
      화면에 <select> 드롭다운 생성

  ┌─────────────────────────────────────────────────────────────┐
  │ <select name="approvalLineConfigId">                        │
  │   <option value="5">일반 결재선</option>                    │
  │   <option value="6">긴급 결재선</option>                    │
  │ </select>                                                    │
  └─────────────────────────────────────────────────────────────┘
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 2️⃣사용자 액션: 결재선 선택 (예: "일반 결재선" 선택)         │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      JavaScript: selectApprovalLine() 실행
                          ↓
      선택된 값: approvalLineConfigId = 5
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 3️⃣사용자 액션: 휴가 신청 버튼 클릭                          │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      FormData 생성:
      {
          "type": "FULL",
          "startDate": "2026-02-20",
          "endDate": "2026-02-21",
          "reason": "개인 사유",
          "approvalLineConfigId": "5",  ← 여기!
          "scheduleDateList": "[...]",
          "fileList": [...]
      }
                          ↓
      POST /api/vacation/save (multipart/form-data)
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 4️⃣VacationApiController.saveVacation()                     │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      IntegratedVacationDTO.convertByHttpRequestParam(fileRequest, request)
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 5️⃣HTTP 파라미터 → DTO 변환 (line 92)                        │
  └─────────────────────────────────────────────────────────────┘

  // IntegratedVacationDTO.java:92
  .approvalLineConfigId(Long.valueOf(request.getParameter("approvalLineConfigId")))
                          ↑
                  request.getParameter("approvalLineConfigId")
                  → "5" (String)
                          ↓
                  Long.valueOf("5")
                  → 5 (Long)
                          ↓
      IntegratedVacationDTO {
          userId: 1,
          type: FULL,
          startDate: "2026-02-20",
          endDate: "2026-02-21",
          reason: "개인 사유",
          approvalLineConfigId: 5,  ← DTO에 저장됨!
          ...
      }
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 6️⃣Chain 실행: handler.process(dto)                         │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      VacationValidation.process(dto)  ✅
                          ↓
      IntegratedVacationService.process(dto)  ✅
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 7️⃣ApprovalService.process(dto)                             │
  └─────────────────────────────────────────────────────────────┘
                          ↓
      ApprovalDTO approvalDTO = request.makeApproval();
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 8️⃣IntegratedVacationDTO.makeApproval() (line 108-117)      │
  └─────────────────────────────────────────────────────────────┘

  @Override
  public ApprovalDTO makeApproval() {
      return ApprovalDTO.builder()
              .requestId(this.getId())              // 123 (휴가 ID)
              .requesterId(this.getUserId())        // 1 (홍길동)
              .approvalRequestType(getApprovalRequestType())  // VACATION
              .requestType(this.getRequestType())   // NEW
              .approvalLineConfigId(this.getApprovalLineConfigId())  ← 여기서 전달!
              .build();                                              // 5
  }
                          ↓
      ApprovalDTO {
          requestId: 123,
          requesterId: 1,
          approvalRequestType: VACATION,
          requestType: NEW,
          approvalLineConfigId: 5  ← ApprovalDTO에 전달됨!
      }
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 9️⃣ApprovalService.registerApprovalAndGetId()               │
  └─────────────────────────────────────────────────────────────┘

  private Long registerApprovalAndGetId(AttendanceDTO request) {
      ApprovalDTO approvalDTO = request.makeApproval();  ← approvalLineConfigId: 5

      Long newApprovalId = insertApproval(approvalDTO);
      // → DB Insert: approval 테이블에 approval_line_config_id = 5 저장

      approvalDTO.setId(newApprovalId);
      insertApprovalProcess(approvalDTO);
      // → approvalLineConfigId = 5를 사용하여 결재 프로세스 생성

      return newApprovalId;
  }
                          ↓
  ┌─────────────────────────────────────────────────────────────┐
  │ 🔟 insertApprovalProcess(approvalDTO)                       │
  └─────────────────────────────────────────────────────────────┘

  private void insertApprovalProcess(ApprovalDTO request) {
      // ① approvalLineConfigId = 5를 사용하여 결재선 설정 조회
      List<ApprovalDetailConfig> approvalDetailConfigList =
          getApprovalDetailConfigList(request);
                          ↓
      // ② approval_line_config 테이블 조회
      SELECT * FROM approval_line_config WHERE id = 5;
                          ↓
      결과: {
          id: 5,
          title: "일반 결재선",
          approvalDetailConfig: [
              {order: 1, type: USER, typeId: 2},   // 김팀장
              {order: 2, type: TEAM, typeId: 10},  // 개발팀
              {order: 3, type: USER, typeId: 3}    // 박임원
          ]
      }
                          ↓
      // ③ REQUESTER 자동 추가
      [
          {order: 0, type: REQUESTER, typeId: 1},  // 홍길동 (신청자)
          {order: 1, type: USER, typeId: 2},       // 김팀장
          {order: 2, type: TEAM, typeId: 10},      // 개발팀
          {order: 3, type: USER, typeId: 3}        // 박임원
      ]
                          ↓
      // ④ approval_process 테이블에 Insert
      INSERT INTO approval_process VALUES (...)
  }


  ---
  🎯 핵심 코드 분석

  1. 화면 (vacation_info.html:119)

  <select class="form-select" 
          id="approvalListSelect" 
          name="approvalLineConfigId"  ← FormData의 key
          onchange="selectApprovalLine(this)">
      <option value="5">일반 결재선</option>
      <option value="6">긴급 결재선</option>
  </select>

  설명:
  - name="approvalLineConfigId" → HTTP 요청 파라미터의 키가 됨
  - 사용자가 "일반 결재선" 선택 → approvalLineConfigId=5가 전송됨

  ---
  2. DTO 변환 (IntegratedVacationDTO.java:83-100)

  public static IntegratedVacationDTO convertByHttpRequestParam(
          MultipartHttpServletRequest fileRequest,
          HttpServletRequest request) throws JsonProcessingException {

      return IntegratedVacationDTO.builder()
              .userId((Long) request.getSession().getAttribute("userId"))
              .type(VacationType.valueOf(request.getParameter("type")))
              .reason(request.getParameter("reason"))
              .requestType(RequestType.valueOf(request.getParameter("requestType")))
              .year(Integer.valueOf(request.getParameter("year")))

              // ⭐ 여기서 HTTP 파라미터를 가져옴!
              .approvalLineConfigId(Long.valueOf(request.getParameter("approvalLineConfigId")))

              .scheduleDateList(objectMapper.readValue(
                  request.getParameter("scheduleDateList"),
                  new TypeReference<List<VacationScheduleDTO>>() {}))
              .deletedFiles(objectMapper.readValue(
                  request.getParameter("deletedFileList"),
                  new TypeReference<List<Long>>() {}))
              .registeredFiles(objectMapper.readValue(
                  request.getParameter("registeredFileList"),
                  new TypeReference<List<Long>>() {}))
              .multiFiles(fileRequest.getFiles("fileList"))
              .startDate(request.getParameter("startDate"))
              .endDate(request.getParameter("endDate"))
              .build();
  }

  동작:
  request.getParameter("approvalLineConfigId")  // "5" (String)
      ↓
  Long.valueOf("5")  // 5 (Long)
      ↓
  IntegratedVacationDTO.approvalLineConfigId = 5

  ---
  3. ApprovalDTO 생성 (IntegratedVacationDTO.java:108-117)

  @Override
  public ApprovalDTO makeApproval() {
      return ApprovalDTO.builder()
              .id(this.getApprovalId())
              .requestId(this.getId())              // 123 (휴가 ID)
              .requesterId(this.getUserId())        // 1 (홍길동)
              .approvalRequestType(getApprovalRequestType())
              .requestType(this.getRequestType())

              // ⭐ IntegratedVacationDTO에서 ApprovalDTO로 전달!
              .approvalLineConfigId(this.getApprovalLineConfigId())  // 5

              .build();
  }

  ---
  4. 결재 프로세스 생성 (ApprovalService.java:130-136)

  private List<ApprovalDetailConfig> getApprovalDetailConfigList(ApprovalDTO request) {
      // ⭐ approvalLineConfigId를 사용하여 결재선 설정 조회
      Long configId = request.getApprovalLineConfigId();  // 5

      ApprovalLineConfig approvalLineById =
          approvalLineConfigRepository.findApprovalLineById(configId);
          // → SELECT * FROM approval_line_config WHERE id = 5;

      List<ApprovalDetailConfig> approvalDetailConfig =
          approvalLineById.getApprovalDetailConfig();
          // → [김팀장, 개발팀, 박임원]

      // REQUESTER 자동 추가
      approvalDetailConfig.add(0,
          ApprovalDetailConfig.makeRequesterApprovalConfig(request.getRequesterId()));
          // → [홍길동(신청자), 김팀장, 개발팀, 박임원]

      return approvalDetailConfig;
  }

  ---
  ★ Insight ─────────────────────────────────────

  5. 왜 화면에서 approvalLineConfigId를 전달하는가?

  사용자 선택권 제공:

  사용자가 상황에 따라 다른 결재선을 선택할 수 있음:
  - 일반 휴가: "일반 결재선" (팀장 → 부서장)
  - 긴급 휴가: "긴급 결재선" (팀장만)
  - 장기 휴가: "임원 결재선" (팀장 → 부서장 → 임원)


  ---
  2. 백엔드에서 자동으로 결재선을 정하지 않는 이유

  안 좋은 설계 (자동 선택):
  // ❌ 백엔드가 무조건 기본 결재선 사용
  ApprovalLineConfig defaultLine =
      approvalLineConfigRepository.findDefaultByUserId(userId);

  문제점:
  - 사용자가 선택할 수 없음
  - 긴급 상황에 빠른 결재선을 사용하지 못함
  - 유연성 부족

  좋은 설계 (현재 구조):
  // ✅ 화면에서 사용자가 선택한 결재선 사용
  Long configId = request.getApprovalLineConfigId();  // 화면에서 전달됨

  장점:
  - 사용자가 상황에 맞게 선택
  - 긴급/일반/장기 등 다양한 시나리오 대응
  - 유연성 확보

  ---
  3. 화면 로딩 시 결재선 목록 조회

  화면 로딩 시 (vacation_info.html):
  // 사용자의 결재선 목록 가져오기
  GET /api/approval/getLineConfigByRequesterId

  Response:
  [
      {
          "id": 5,
          "title": "일반 결재선",
          "lineType": "DEFAULT",
          "approvalDetailConfig": [
              {"orderNumber": 1, "type": "USER", "typeId": 2, "name": "김팀장"},
              {"orderNumber": 2, "type": "TEAM", "typeId": 10, "name": "개발팀"},
              {"orderNumber": 3, "type": "USER", "typeId": 3, "name": "박임원"}
          ]
      },
      {
          "id": 6,
          "title": "긴급 결재선",
          "lineType": "CUSTOM",
          "approvalDetailConfig": [
              {"orderNumber": 1, "type": "USER", "typeId": 2, "name": "김팀장"}
          ]
      }
  ]

  드롭다운 생성:
  <select name="approvalLineConfigId">
      <option value="5">일반 결재선 (김팀장 → 개발팀 → 박임원)</option>
      <option value="6">긴급 결재선 (김팀장)</option>
  </select>

  ---
  4. 데이터 흐름의 일관성

  HTML Form
      ↓ (name="approvalLineConfigId")
  HTTP Request Parameter
      ↓ (request.getParameter("approvalLineConfigId"))
  IntegratedVacationDTO
      ↓ (this.getApprovalLineConfigId())
  ApprovalDTO
      ↓ (request.getApprovalLineConfigId())
  DB Query (findApprovalLineById)
      ↓
  approval_line_config 테이블 조회
      ↓
  ApprovalDetailConfig List
      ↓
  approval_process 테이블 Insert


  핵심: approvalLineConfigId는 화면부터 DB까지 일관되게 전달되며, 중간에 변환되거나 수정되지 않음

  ────────────────────────────────────────

  💡 요약

  approvalLineConfigId의 출처

  ✅ 화면(HTML)에서 사용자가 선택
  → <select name="approvalLineConfigId" value="5">

  ✅ HTTP 요청 파라미터로 전달
  → POST /api/vacation/save?approvalLineConfigId=5

  ✅ IntegratedVacationDTO로 변환
  → Long.valueOf(request.getParameter("approvalLineConfigId"))

  ✅ ApprovalDTO로 전달
  → this.getApprovalLineConfigId()

  ✅ DB 조회 및 결재 프로세스 생성
  → findApprovalLineById(5)


  핵심: 백엔드가 자동으로 정하는 것이 아니라, 사용자가 화면에서 선택한 값이 전달되는 구조입니다!
