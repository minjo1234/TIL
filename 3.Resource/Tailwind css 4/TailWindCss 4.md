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
''
- 1.1층 관제실에서 clovirone 모니터링 이용하여 관제할 예정이다.
- 2.L4  - 장비,서비스별의 헬스체크가 가능한지  - 테이블로 가시성있도록 확인 
- 3.특정 시간대의 배포는 추후의 사업에서 정의 
- 4.계정관련정보는 이철규 대리님에게 문의하도록 하기.
- 5.포탈 확인해볼것 - 개발망
- 6.운영망 배포일정

- 금주 진행예정, 목요일 제외하기. 
- DataCenter와 APIC을 연결하지 않고, 다른 API를 사용해서 해결할 수 있는지 확인하기. 
- 승인 프로세스가 결정되지 않음. (공사, 시설)  
	- 신청서 양식이 다르다. 
- 배포 프로세스가 결정되지 않음. 



-----


























