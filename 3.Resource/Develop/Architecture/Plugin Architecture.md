
SPI(Service Provider Interface)
- 프레임워크는 인터페이스(정의)를 제공하고,
- 외부 개발자가 그 구현체(기능)를 만들어 끼워 넣을 수 있도록 설계된 지점을 의미한다.

일반적인 프로그램은 메인 코드가 외부 라이브러리를 호출(Import)하지만, SPI 기반 아키텍처에서는 이 의존성 방향이 뒤집힙니다. (IoC)


플러그인 간의 의존성 충돌(Dependency Hell)은 어떻게 해결하나요?
- **의도:** 플러그인 A와 B가 서로 다른 버전의 라이브러리(예: Jackson 2.9 vs 2.12)를 사용할 때 발생하는 문제를 묻는 것입니다.
- **답변 전략:** "각 플러그인을 **독립적인 클래스로더(Class Loader)**로 격리하여 로드합니다. Java의 경우 OSGi나 정교한 ClassLoader 설계를 사용하고, 최근에는 컨테이너 기반(Sidecar) 방식도 고려합니다."


### 메인 시스템과 플러그인 사이의 데이터 교환(Communication)은 어떻게 이루어지나요?"

- **의도:** SPI 규격(Interface)이 너무 복잡하거나 자주 바뀌지 않는지 확인하려는 것입니다.
- **답변 전략:** "엄격하게 정의된 **DTO(Data Transfer Object)와 Interface**를 통해서만 소통합니다. 메인 시스템은 플러그인에 'Context' 객체를 넘겨주고, 플러그인은 정해진 'Result' 객체를 반환하는 구조입니다." , 의존성이 높아질만한 에로사항을 만들지 않는 것 입니다.

### 플러그인이 너무 많아지면 성능 저하(오버헤드)가 발생하지 않나요?"

- **의도:** 동적 로딩과 인터페이스 호출에 따른 비용을 묻는 것입니다.
- **답변 전략:** 플러그인 로딩은 초기 구동 시에만 호출하여 성능에 대한 문제는 발생하지 않습니다.


1.CustomAction
2.Infra, genera action 
- general -> portal 
- Infra -> Custom 으로 변경예정이다.
- default action 
- custom action - 자원권한체크 
- 


---
1.ag-grid, 그리드를 고려해서
현재 페이지에서 마지막데이터를 조회할때 

---


1.첫 클릭시에는 나오지마 날짜를 변경할 경우 
- 자신의 데이터로 변경되는 것을 확인했다.

2.그룹별 일정 
- 데이터 조회속도가 느리다. -> 속도 개선이 필요하다. 
- 확장버튼이 존재하지 않는다. 

3.나의 일정에서 특정 사용자 조회시에 조회 속도가 느리다.
- 전체 일정으로 가는것이 아닌 나의 일정 (한달치의 정보가 나의 일정 형태로 나오도록 설정하기.) 

4.연간일정, 주간일정 고려해서 만들기.
- 주간일정 : 주 일정 
- 연간일정 : 월별일정 

5.문의사항이 올라올 경우 
- 배포일시, 조치내용에 대한 확인에 대한 comment 남겨주기.



  Skill이 맞는 경우                                                                                                                                                                      
  - 여러 프로젝트에서 재사용 가능한 범용 워크플로우
  - 명시적 호출(/playwright)이 필요한 독립적 기능
  - 플러그인 인프라(plugin.json 등) 관리 비용을 감수할 가치가 있을 때


조인어스비즈
야간에 
Database 별도로 분리된다. 
- datbase는 빈 내역으로 전송해도 상관없다.



```

```


TypeScript 

- Partial : 해당 객체중 모든 객체의 요소가 아닌 입력받고 싶은것만 입력받도록 설정된다.
- overrides: 해당 값은 덮어씌워 질 예정인 값을 의미한다.


Supabase 
- Wlgns3350@@

. /hookify 명령어 - 대화 기반으로 훅 자동 생성

  - 타입/린트 검사 (빠름, 즉각적)
  - 단위 테스트 (Jest)
  - UI 스냅샷/E2E (Playwright, 느리지만 강력)
  - 위 전부 조합



  ---
  수정 순서 (4단계)

  Step 1 — package.json scripts 수정 (1줄)
  - "lint": "eslint src --ext .ts,.tsx" → "eslint src/"
  - "lint:fix" 동일하게

  Step 2 — qa-check.sh 버그 수정 (2줄)
  - set -euo pipefail → set -uo pipefail
  - __tests__ 경로 패턴 수정

  Step 3 — BMI 로직 버그 수정
  - src/utils/weight.ts 의 calculateBmi 아시아 기준 경계값 확인 및 수정
  - Jest 테스트 통과 확인

  Step 4 — 전체 검증
  - npm run type-check ✅
  - npm run lint ✅
  - npm run test ✅


tsc --noEmit : 문법상 틀린것이 있는지 확인한다.
ESLint : 코드 컨벤션 및 위험 패턴 차단
Jest : 비즈니스 로직 및 기능 작동 검증

`Jest`가 **유닛(단위) 테스트**라면, 앱의 전체 흐름을 테스트하는 것은 **E2E(End-to-End) 테스트**라고 부릅니다.

Detox :  는 E2E 테스트 프레임워크입니다.
 - React Natvie 와 가장 궁합이 좋다.
-

---

Oauth Client Id : 538548591814-2icp52hchpjtaatdg1c8vjrmojoan8tt.apps.googleusercontent.com

Oauth Client Password : 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



```

```

  ★ Insight ─────────────────────────────────────                                                                                                                                                          
  헬스장 기구 데이터는 Life Fitness, Technogym 같은 브랜드들이 공개 API를 제공하지 않아요. 웹 크롤링은 ToS 위반 위험 + 마크업이 바뀌면 깨짐 → 유지보수 비용이 큼. 현실적인 "자동화"는 데이터 소스를        
  JSON/CSV로 관리 + 파이프라인 스크립트로 Supabase에 자동 적재하는 구조예요 — 새 기구 추가 = JSON 수정 → CI/CD가 자동 sync.  

upsert하는?


---

특정 클러스터의 메모리 사용률 확인ㄴ

kubectl top node gpu-tkc-gpu-t4-2-mtcf4-dc4d57d57-lrsd8

pod 조회

kubectl describe pod app-wozqlrbkccrcvnu-5b8c8b66-cqpx8 -n gpu-ncdc2025110002

Last State:     Terminated
      Reason:       Error
      Exit Code:    137
      Started:      Tue, 24 Feb 2026 14:26:51 +0900
      Finished:     Tue, 24 Feb 2026 14:28:06 +0900
    Ready:          False
    Restart Count:  59

쿠버네티스 시스템에 의해 강제종료를 당했다. 

Liveness = 살아있는지 판단하기.
15초보다 길면 죽었다고 판단한다. liveness 가 15초보다 길 경우에는


1.isGpuOperator와 isGpuNode는 서로 다른 GPU 배포 방식을 구분: Operator는 Kubernetes GPU Operator로 관리되는 환경, Node는 GPU 노드에 직접 배포하는 환경

2.isGpuNode 

isGpuNode - GPU 노드에 직접 배포한다. - GPU_EA =  1 요청
isGpuOperator - Kubernetes GPU Operatro , GPU 수량은 0 이다.

- CM_TMPL.GPU_YN -> isGpuNode 
- CM_CLUSTER.GPU_USE_YN ->


  // ParseTemplate.java:65
  if(yaml.indexOf("GPU_EA") > 0 && yaml.indexOf("GPU_SELECTOR") > 0) {
      result.put("GPU_YN", "Y");   // YAML 안에 GPU_EA, GPU_SELECTOR 변수가 있으면 GPU 템플릿
  }

obj.isGpuCluster = isGpuNode 
obj.isGpuOperator = isGpu_YN

1.Node에 Gpu개수가 몇개남았는지 확인할 수 있도록 해야하나 ? 

- GPU 1 개짜리 노드 여러 개로 구성된 경우 


---

AS-IS 

- 내부 : 하버 + 내부 Nexus -  VM 
- 외부 : Nexus  - 물리서버 (신상규 과장님이 진행예정)

내부 Nexus 에서 -> 외부 Nexus에서 바라보고 있다.


TO-BE 

해야 할 작업 

- 외부 Nexus 에 대한 설치 (문의) 
- Nexus 백업 및 복원 - 진행예정


1.Nexus, 하버 분리예정 

서버 구성 : Git, DB, WAS, Nexus, 하버, boot 
임시 IP는 모두 할당 될 예정이다.



