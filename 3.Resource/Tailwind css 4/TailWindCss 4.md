1.tailwindCss 설정

만약 Tailwind CSS v4를 사용 중이라면, 이제 기존의 `tailwind.config.js` 파일 없이도 CSS 파일 내에서 직접 설정을 제어할 수 있습니다.

무한스크롤일때는 excludeIds가 필수적이다.
- 전체 선택을 누르고 해당건만 제외한 다음에 보내면 되기 때문임.


 MULTI_SELECT.md 파일을 살펴보고 selectedRow 를 selectedRows 로
  현재 selectedRow를 사용하는
  /Users/jomin/Desktop/clovirone/clovirone-base/clovircm-web/src/ma
  in/resources/templates/clovirone/state/project/aria/index.ftl
  여기부터 변경하려고해 

- OS 자동화도 추후 고려하여 MULTI_Select 시 고려한다.
- VM List 컴포넌트에 태그 달아둔다.

---

``

마이크로 서비스 
save - Redis 
save - RabbitMq 
save - MariaDB 
save - OracleDB 

현재 구조에서 인프라적인 변화때문에 문제가 발생할 수 있다.
save()로직의 많은 수정이 일어나기 때문이다.
하지만 Adpater를 둘 경우에 구현체에 따라서 작동하는 save()로직이 다르기 때문에 결합도가 낮아진다. 

```java
public class OrderService {
    // 기술이 바뀔 때마다 이 부분을 계속 수정해야 함!
    // private final MariaDbClient client; 
    private final RedisClient client; // Redis로 바꾸느라 고생 중...

    public void saveOrder(Order order) {
        client.set(order.getId(), order); // 기술 전용 메서드에 종속됨
    }
}
```

/api/aria/request/multi-actionx

- /api/gpu/vm/state/uuids -> 해당 메서드에 대한 controller 및 서비스 구현필요
- gpuVm은 uuid를  사용하지 않는 것으로 확인되었음. ariaResourceUuid
	- resourceUuid, deploymentUuid를 사용함
	- action에서 resourceUuid, deploymentUuid중에서 뭐를 사용하는 지 파악해야한다.
	- vmView.class에서 resourceUuid 가 없는데 어떻게 openChart(vm) 에서 resourceUuid를 가져와서 사용이 가능했던걸까 ?
	- 

우리 회사는 휴가쓴거랑 상관없이 동일임금































요구사항 -> PM <-> 팀원끼리 
마켓컬리 TPM <-> (PM + 팀원)


- 스마일게이트 통합테스트
- 새마을금고 MG (이거나네 ?)
- 암센터도 나임 ? 

---

화요일 10시에 ICT에서 인천공항 관련 회의예정

 1.요구사항에 ACI/L4 모니터링 구현이라고 되어있지만, 요구사항 협의에 나온 내용은 ACI만 사용하면 되는 것이라서 추가로 구현할 것은 없는지 ?
2.L3 관련한 요건은 추가적으로 존재하는 것인지 ? 
3.적정사이즈 제안에 대해 개발이 필요한지 ?  
4.시스템로그를 어떻게 처리할 것인지 

### 📋 인천공항 회의 핵심 질문 (4가지)

1. **[모니터링]** 요구사항엔 'ACI/L4'지만 협의 시 나온 내용은 ACI만으로 구현이 가능하다. → **L4 모니터링 제외 확정인가요?**
2. **[L3 요건]**  **L3 레이어 관련 추가 요구사항**이 있나요?
3. **[사이즈 제안]** 적정 사이즈 제안 기능은 Operation이 존재하지 않아서 구현이 어려우며, 구현이 원할경우 어떤식으로 구현해드리길 원하는지
4. **[로그 처리]** 시스템 로그 수집은 불가능하다.

------

### 1.

- 1.1층 관제실에서 clovirone 모니터링 이용하여 관제할 예정이다.
- **2.L4  - 장비,서비스별의 헬스체크가 가능한지**  - 테이블로 가시성있도록 확인 
- 3.특정 시간대의 배포는 추후의 사업에서 정의 
- 4.계정관련정보는 이철규 대리님에게 문의하도록 하기.
- 5.포탈 확인해볼것 - 개발망
- 6.운영망 배포일정

- 금주 진행예정, 목요일 제외하기. 
- DataCenter와 APIC을 연결하지 않고, 다른 API를 사용해서 해결할 수 있는지 확인하기. 
- 승인 프로세스가 결정되지 않음. (공사, 시설)  
	- 공사 -> SSO
	- 시설 -> 자체 로그인으로 이용 
	- 신청서 양식이 다르다. 
- 배포 프로세스가 결정되지 않음. 
- system_log -> 키위(kiwwiy) 
- 14:00~15:00 

이재연 차장님과 회의 

- 어떻게 할 지 구체적인 내용이 나와야한다.
- 애프터서비스로 할 건지 
- 초안정도는 이번달말에 나올 것 같다. 
- 크게 2가지가 존재한다. 
	- 신청에 대한 부분, 현황관리에 대한 부분 
	- 어떤 현황을 어떻게 관리할지 엑셀로 정리해서 드리고 싶은데, 현재는 여력이 없다.
	- 이달말에서 2월초까지는 해야한다 
	- SSO 연동이 가능한 지, 
	- 신청하는 화면이, Clovirone과 다른데 , 등록되는 항목이 다른데 SSO로 할때 공사쪽에서 사용하던 것을 Clovirone으로 바로 가져올지 고민을 할 예정이다.
	- AD는 없음. 
	- 추가 사업으로 할지안할지에 대한 논의이다.
	- 

-----


9 인천공항 운영망 재배포 
14 새마을금고 
15 암센터 

노트북 인터넷진흥원,

----
1.작업일정 : X 
2.enable 할 시에는 포트그룹이 할당이 되는데, 
3.현재 resource도 많이 사용하고 있는 상태라서, 최대한 정책 추가를 지양하고 있다.

정확히 말씀드리면, **Controller, Spine, Leaf, Border-Leaf는 L4 장비 내부의 구성 요소가 아니라, 그 L4 장비가 연결되어 있는 'Cisco ACI 네트워크 전체 인프라'의 구성 요소**

고객사에서 원하는게
APIC에 연결된 CISCO ACI 네트워크 전체 인프라인지
APIC에 연결된 L4 장비가 연결되어 있는 Cisco ACI 네트워크 전체 인프라인지,
L4 장비의 내부의 구성요소인지

- 오픈웨이 시스템 지원

-----


- apic <-> 

간혈적으로 전체 체크박스가 해제되지 않는 현상이 있다.
1.전체 check box 선택  -> 전체 체크박스가 유지
2.단일 checkbox 선택 -> 전체 체크박스가 해지되고
3.전체 체크박스 선택 -> 전체 체크박스 유지
4.단일 checkbox 선택 -> 전체 체크박스가 유지된다.

전체 체크박스 헤제됨, 해당 상태에서 전체체크박스 선택 -> 다시 전체 체크박스 선택된다. -> 여기서 하나풀기 

- formatting 확인
- ㅌ




---

1.발리 - 
- 4주
- 서핑캠프 2주 

2.일본 
- 일주일이내 

3.중국 
- 일주일이내 

4.호주 

1. 노코드(No-code)와 로코드(Low-code)의 융합: **Rive & Framer**
2. 1. 3D와 공간 설계의 정점: **Three.js & Spline**

---

message.properties 에 true, false 

---

NextHub 

1.수주완료 상태일경우 - 수주완료보고서 확인필요 
2.영업실적 -> 통계가 안 맞음.

---

이현아 전무님


1.영업실적 금액이 맞지않음. 우선협상 금액이 맞지않음 확인할 것 - 체크 할것
2.매출품목 수정 - 대표님 엑셀과 맞지않는 것들이 다수 존재한다.
- 현재는 벤더사 기준으로 작성되어 있다.
- 

3.사업자 등록이후 바로 업데이트가 되지않는다. 
- 캐싱처리를 확인해보기.

4.발행완료건과 영업실적과의 금액이 맞지않음.
- 체크할것 (매출발행 탭과 금액비교해보기.)

5.매출발행은 
- 착수금
- 중도금 
- 잔금 으로 받는 경우가 존재하는데, 

---
### 매입 

- 매입에서 자동으로 계속 잉여데이터가 발생한다.
- 내부에서 취소가 가능하도록 설정하기.  - 취소만들어두기. 
- 내일 다시 생기는지 확인하기. 
- 착수금 중도금 잔금이 있으면 좋겠다.  - **단일로 하자 내가 할 거 없을듯** 
- 매출발행 등록과, 매입에 비고가 있으면 좋겠다. - 

---

4.영업실적에서는 세금제외하기
- 영업실적은 세금을 제외한다.


1.사업자등록 후, 사업자가 바로 보이지 않음 - 테스트 이상없음
2.

---

docker 설치 

### 1. 다운로드해야 할 파일 5개 (Noble 기준)

1. **containerd.io** (스크롤 중간쯤)
    - `containerd.io_1.7.27-1_amd64.deb` (또는 버전 숫자가 더 높은 것)
2. **docker-ce** (더 아래로 내려가세요)
    - `docker-ce_28.0.4-1~ubuntu.24.04~noble_amd64.deb`
3. **docker-ce-cli**
    - `docker-ce-cli_28.0.4-1~ubuntu.24.04~noble_amd64.deb`
4. **docker-buildx-plugin**
    - `docker-buildx-plugin_0.21.1-1~ubuntu.24.04~noble_amd64.deb`
5. **docker-compose-plugin**
    
    - `docker-compose-plugin_2.32.4-1~ubuntu.24.04~noble_amd64.deb`
---

1.우선협상 단계가 되었으면 -> 수주완료 -> 발행완료 
2.수주완료 


8443 



dns : "0.0,0,0"

- 프로비저닝 관리 


- 수동배포 

