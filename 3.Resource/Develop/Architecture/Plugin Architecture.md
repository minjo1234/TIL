
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


- 내부 Nexus 에서 -> 외부 Nexus에서 바라보고 있다.


TO-BE 

해야 할 작업 

- 외부 Nexus 에 대한 설치 (문의) 
- Nexus 백업 및 복원 - 진행예정

1.Nexus, 하버 분리예정 

서버 구성 : Git, DB, WAS, Nexus, 하버, boot 
임시 IP는 모두 할당 될 예정이다.
암센터 이관작업



App Code : app-yljmpvncqlltpge

참조 파일 

- stepTwo.jsp  -> gpu_ea 
- newApp_step_pop.jsp 


stepTwo.jsp 

- gpu_ea 추가 

```jsp
<label for="gpu_ea" class="control-label grid-title value-title" style="text-align: left; margin-left: 10px;">GPU 수량</label>  
<input type="number" class="form-control input" id="gpu_ea" name="GPU_EA" value="0" min="0" max="1" style="width: 80px; display: inline-block;">

```


java.lang.RuntimeException: java.lang.StringIndexOutOfBoundsException: String index out of range: -1

[GC (Allocation Failure)  745726K->138768K(867840K), 0.0054614 secs]
org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.exceptions.TooManyResultsException: Expected one result (or null) to be returned by selectOne(), but found: 2

간시엔 니 징티엔 신친 공쥬어

간~시엔! 니 징티엔


뽀우 포우 모우 풔우 더 터 너 러 그어 크어 흐어 지
b  p m f d t n l g k h j

치 시 즐 츨 싈 릐어 즈 츠 스 이 우
q x zh ch sh r z c s y w 

아 오어 으어 이에 우 의에 
a o e i u u

아이 에이 왜이 아우 어우 이유 이에 의에 얼 
ai ei ui ao ou iu ie ue er 

안 언 인 운 읜 
an en in un un 

앙 엉 잉 옹 
ang eng ing ong

즐 츨 싈 르 즈 츠 쓰 이 우
zhi chi shi ri zi ci si  yi

의 이에 유에 유안 인 읜 잉 
	yu ye yue yuan yin yun yxin                 







小薇为什么要学韩语？
Xiǎo wēi wèishéme yào xué hányǔ?


如果 -  rúguǒ , 만일
很好 - Hěn hǎo 매우 좋은
云粉
看 - Kàn 보다 
脸 - liǎn 얼굴
见面 - Jiànmiàn 만나다.
学习 - Xuéxí 공부 
不一样 - Bù yīyàng 다른 
明白 - míngbái 이해하다
开心 - Kāixīn 행복하다.
帅 - Shuài 멋있는
晚安 - Wǎn'ān , Goodbye
我会 - Wǒ huì  나는 ~ 할 수 있다.
**读 (dú)：** 读 / 阅读 (read)
**和 (hé)：** 和 / 以及 (and)
写 -  xiě  read 
**这些 (zhèxiē)：** 这些 (these)
**真 (zhēn)** really
**厉害 (lìhai):** awesome 



**学 (xué)：** 学习 (learn)
**zhǔnbèi (准备):** 준비하다
**qù (去):** 가다
**shuìjiào (睡觉):** 자다, 잠자다
**le (了):** (상황의 변화나 완료를 나타내는 어기조사)

晚安 ： Wǎn'ān ， 안녕히 주무세요

**做 (zuò):** 하다, 꾸다 (꿈을 꾸다 할 때 쓰임)
**个 (gè):** 하나, 개의 (꿈을 셀 때 쓰는 양사)
**好梦 (hǎo mèng):** 좋은 꿈

做个好梦 (zuò gè hǎo mèng)

**shuì** vs **shuìjiào**
Wǒ huì  vs wo 可以 


你睡得好吗？
**睡得好吗？**【shuì de hǎo ma？】
真的吗 Zhēn de ma, 정말로 ?
午饭 Wǔfàn, 점심 
你吃午饭了吗 Nǐ chī wǔfàn le ma?) , 점심먹었어?
**나 출근했어:** 我上班了 (Wǒ shàngbān le), 워 샹빤러
**나 퇴근했어:** 我下班了 (Wǒ xiàbān le), 워 씨아빤 러 
**오랜만이야:** 好久不见 (Hǎojiǔ bùjiàn) , 하오지오 부지엔 
**반가워:** 很高兴见到你 (Hěn gāoxìng jiàndào nǐ) 헌 

까오 싱 지엔 따오 니

- **上班 (샹빤):** 출근하다 (동작 그 자체)
- **上班了 (샹빤 러):** 출근했다 (출근하지 않은 상태 → **출근한 상태로 변화**)

- **吃 (츠):** 먹다
- **吃饭了 (츠판 러):** 밥 먹었다 (배고픈 상태 → **배부른 상태로 변화**)

qi

**请给我两碗米饭。** (칭 게이 워 리앙 완 미판) **Qǐng gěi wǒ liǎng wǎn mǐfàn.**



1.이게 뭐야 ?
2.조금
3.많이 
4.엄청

엄청 조금 





GPU 개수를 조절하는 과정에서 에러가 발생함.

- Exit Code:  137 (OOM Killed)
- GPU -> CPU로 바꾸는 과정에서 RAM이 증가한 거 아닐까라는 판단
- Status:   Failed
- Reason: ContainerStatusUnknown
- Reason: Evicted
- Message:  The node was low on resource: ephemeral-storage (임시 저장소)

Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Tue, 10 Mar 2026 09:52:37 +0900   Sat, 20 Sep 2025 02:37:28 +0900   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Tue, 10 Mar 2026 09:52:37 +0900   Sat, 03 Jan 2026 21:14:29 +0900   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Tue, 10 Mar 2026 09:52:37 +0900   Sat, 20 Sep 2025 02:37:28 +0900   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Tue, 10 Mar 2026 09:52:37 +0900   Sat, 20 Sep 2025 02:37:49 +0900   KubeletReady                 kubelet is posting ready status. AppArmor enabled


Terminating -> ContainerCreating 
PostStartHookError
CrashLoopBackOff

| **상황**                | **권장 조치**         | **이유**               |
| --------------------- | ----------------- | -------------------- |
| **코드 에러/오류**          | 코드 수정 후 재배포       | 근본적인 해결책             |
| **리소스 부족 (OOM/Disk)** | 리소스 `limits` 증설   | 환경에 맞게 리소스 조정        |
| **일시적 노드/네트워크 장애**    | **`delete` (교체)** | 노드 교체 시 정상 노드로 스케줄링됨 |
| **설정(Config) 실수**     | `edit` / `patch`  | 굳이 삭제하지 않아도 수정 가능    |



kubectl get nodes -o custom-columns=NAME:.metadata.name,GPU:.status.allocatable.nvidia\.com/gpu 

gpu 사용가능한 node 를 파악

This is a classic Kubernetes **rolling update conflict**. Here's what likely happened:

resourcequota

1.new pod request `GPU: 1` request 
2.Kubernetes Schedular watch the node 
3.


when I deleted pod, deployments make a pod 

---

단어 하나하나의 의미를 정확히 파악하면 문장이 훨씬 더 잘 외워질 거예요! 질문하신 단어들을 쪼개서 설명해 드릴게요.

### 1. 好久不见 (Hǎojiǔ bùjiàn)

이 문장은 세 부분으로 나뉩니다.

- **好 (hǎo, 하오):** '매우', '아주'라는 뜻입니다.
- **久 (jiǔ, 지우):** '오래되다', '긴 시간'이라는 뜻입니다.
    - 그래서 **好久(하오 지우)**를 합치면 **"매우 긴 시간"**이 됩니다.
- **不 (bù, 부):** '아니다', '않다'라는 부정어입니다.
- **见 (jiàn, 지엔):** '보다', '만나다'라는 뜻입니다.
    - 그래서 **不见(부 지엔)**은 **"만나지 못했다"**는 뜻이 됩니다.

즉, **"아주 긴 시간 동안 만나지 못했네"**가 되어, 우리가 쓰는 **"오랜만이야"**가 되는 것이죠!

---

### 2. 很高兴见到你 (Hěn gāoxìng jiàndào nǐ)

이 문장도 하나씩 뜯어볼까요?

- **很 (hěn, 헌):** '매우', '아주' (영어의 very와 같아요)
- **高兴 (gāoxìng, 까오싱):** '기쁘다', '즐겁다'
    - 합치면 **很高兴(헌 까오싱) = 매우 기쁘다**
- **见到 (jiàndào, 지엔따오):** '만나다'
    - **见(지엔)**이 '보다'라면, **见到(지엔따오)**는 '보아서 ~에 도달하다', 즉 **'만나다'**라는 결과적인 의미가 강해요.
- **你 (nǐ, 니):** '너'

결국 **"매우 기쁘다 / 만나서 / 너를"** 순서로 해석되어 **"너를 만나서 매우 기뻐(반가워)"**가 됩니다.

| **단어**  | **발음** | **의미**  |
| ------- | ------ | ------- |
| **好久**  | 하오 지우  | 아주 긴 시간 |
| **不见**  | 부 지엔   | 만나지 못했다 |
| **很高兴** | 헌 까오싱  | 매우 기쁘다  |
| **见到**  | 지엔 따오  | 만나다     |

postStart는 한 번만 반복된다.  when the pod Immediately after created 


쿠버네티스에서의 수정은 수정이 아니라 새로운 컨테이너의 생성이다.
PVC에 마운트가 일어날경우, 새로운 pod에 기존 파드의 pvc와 심볼릭 링크 정보가 그대로 할당된다.
postStart로 이중등록이 아닌 등록이 되어있을 경우를 고려하여 yaml을 작성한다.

문제가 발생했던 이유 pod 수정시에 postStart 로 설정된 옵션에서 심볼릭 링크를 추가로 설정하는데 기존 PVC에 설정되어있기때문에 중복 오류가 발생하였던 것이다.

### 1. "쿠버네티스는 수정이 아니라 생성이다" (정확함)

- **불변성(Immutability):** 쿠버네티스에서 Pod는 '수정' 가능한 객체가 아닙니다. 설정을 바꾸면 이전 Pod는 `Terminating` 되고, 바뀐 설정으로 새로운 Pod가 `Pending` -> `Running` 단계를 거쳐 새로 생성됩니다.

### . "PVC 정보가 그대로 할당된다" (정확함)

- **영구 저장소(Persistence):** Pod가 죽고 새로 태어나도, 동일한 PVC를 마운트하면 그 안에 들어있던 파일과 심볼릭 링크 정보는 그대로 유지됩니다. 이것이 PVC를 사용하는 이유이죠.
- **데이터 보존:** 이전에 실행되었던 `postStart` 스크립트가 만들어놓은 심볼릭 링크 파일(`ls -l`로 확인하신 그 링크)들도 PVC 안에 고스란히 남아있습니다.

### 3. "중복 오류가 발생했던 이유" (정확함)

- **멱등성(Idempotency) 부재:** 이전 스크립트는 `ln -s`를 실행할 때 "이미 있는지"를 확인하지 않고 무조건 실행했습니다.
- **충돌:** 새 Pod가 PVC를 마운트하면 이미 링크가 존재하는데, 그 상태에서 `ln -s`를 또 호출하니 운영체제 입장에서 **"File exists" 에러**를 내뱉은 것이고, 이 에러 코드를 받은 쿠버네티스는 해당 Pod가 정상화되지 않았다고 판단하여 계속 다시 시작(`CrashLoopBackOff`)시킨 것입니다.

### 4. "YAML 수정 전략 (이중등록 방지)" (정확함)

우리가 `[ -e 경로 ] ||` 문법을 사용한 것은, **"시스템 상태가 이미 만들어져 있다면(링크가 있다면) 새로 만들지 말고 건너뛰어라(Skip)"**라는 논리입니다. 이로써 Pod가 몇 번을 새로 태어나도 에러 없이 스크립트가 통과하게 되었습니다.


새 컨테이너가 생성되는 것은 쿠버네티스의 정상적인 동작입니다. **이걸 막을 수는 없습니다.** 대신 **새 컨테이너가 생성되어도 스스로 문제를 해결하고 시작하도록** 스크립트를 짜야 합니다.

- **이 저장소는 Pod가 죽어도 데이터가 삭제되지 않고 남습니다.**
    
- **상황:**
    
    1. 이전 Pod가 실행되면서 `/project/git-gpu-test/lib/python3.10/site-packages`에 링크를 만들었습니다.
    2. 이전 Pod가 죽고 새 Pod가 생성되었습니다.
    3. **저장소(PVC)에는 이전 Pod가 만들어 둔 링크 파일이 그대로 남아있습니다.**
    4. 새 Pod의 `postStart` 스크립트가 실행되면서 다시 `ln -s`를 시도합니다.
    5. 시스템은 **"어? 이미 여기에 파일(링크)이 있는데? 또 만들라고?"**라며 **`File exists` 에러**를 뱉고 실패하는 것입니다.


## Gemini의 응답

네, 바로 그 점이 질문자님을 가장 힘들게 하는 **'핵심 모순'**입니다. 이 문제를 완벽하게 이해하면 이제 쿠버네티스 마스터가 되시는 겁니다!

결론부터 말씀드리면, **"새 Pod가 뜨면서 초기화될 때, 우리가 스크립트로 심볼릭 링크를 '다시 생성'해주면 해결된다"**입니다.

- 새 컨테이너는 심볼릭 링크가 없는 '깨끗한 상태'로 시작합니다.
- 하지만 **이전 Pod가 쓰던 저장소(PVC)에는 링크가 남아있습니다.**
- 따라서 **`postStart` 스크립트가 "저장소에 링크가 이미 있는지 확인하고, 없으면 만들고 있으면 그냥 넘어가는" 똑똑한 동작**을 해야만 Pod가 죽지 않고 정상적으로 실행됩니다.

- **저장소(PVC) 관점:** `데이터_파일`이 `/project/git-gpu-test/src`에 있고, `링크_파일`은 `/project/git-gpu-test/lib/site-packages`에 있습니다.
- **새 컨테이너가 뜰 때:** 컨테이너 내부 파일시스템은 깨끗해도, **PVC가 연결(Mount)되는 순간** 이 파일들과 '링크' 파일은 컨테이너 내부 경로에 짠! 하고 나타납니다.

### 1. 데이터의 흐름

심볼릭 링크는 일종의 **'지름길(Shortcut)'**입니다.

- 심볼릭 링크가 가리키는 **원본 경로**가 PVC 안의 데이터 공간(물리적 디스크)에 있다면,
    
- 심볼릭 링크를 통해 저장한 모든 데이터는 결국 **PVC라는 저장소**에 물리적으로 저장됩니다.
    

### 2. 컨테이너가 바뀌어도 데이터는 그대로

- **기존 컨테이너:** 링크를 통해 `/project/git-gpu-test/lib/site-packages`에 데이터를 저장했습니다. 이 데이터는 링크를 타고 넘어가서 **PVC 물리 디스크**에 기록되었습니다.
    
- **새 컨테이너:** 1. 새 컨테이너가 뜨면 PVC를 다시 마운트합니다. 2. 아까 만들어둔 심볼릭 링크가 PVC 안에 그대로 있으니, 새 컨테이너도 같은 링크를 통해 **같은 물리 디스크 경로**를 바라보게 됩니다. 3. 따라서 새 컨테이너에서 해당 경로에 파일을 만들면, 기존 컨테이너가 썼던 데이터와 **동일한 PVC 공간에 데이터가 쌓이게 됩니다.**

기존의 있던 데이터는 자동으로 마운트되고, 이전 pod 가 사용했던 모든 파일과 심볼릭 링크가 그대로 나타난다.


### 2. 새 컨테이너의 '기본 상태'

새 컨테이너 입장에서 보면:

1. **마운트 전:** 컨테이너 안은 텅 비어 있습니다.
2. **마운트 직후:** PVC에 있던 `link_to_data` 링크가 컨테이너 내부 경로에 **짠! 하고 나타납니다.**

保持沙拉 **bāocài****shālā** ，  양배추샐러드



这是， zhe shi , 이것은 ~이다.
**我有问题" (Wǒ yǒu wèntí)** 또는
是午饭吗， shi wufan ma , 점심이야?
[**神奇**](https://www.google.com/search?q=%E7%A5%9E%E5%A5%87&sca_esv=b5455d2c67d11081&rlz=1C5CHFA_enKR1070KR1070&sxsrf=ANbL-n4yECmic4-IcezshD98c3WvE8VurA%3A1773126577592&ei=scOvaa7HI5Tg2roPzLLESA&biw=1152&bih=1323&ved=2ahUKEwjN7o7d6JSTAxWY1TgGHaH4K7cQgK4QegQIARAC&uact=5&oq=%EC%8B%A0%EA%B8%B0%ED%95%B4+%EC%A4%91%EA%B5%AD%EC%96%B4%EB%A1%9C&gs_lp=Egxnd3Mtd2l6LXNlcnAiFuyLoOq4sO2VtCDspJHqta3slrTroZwyBBAAGB4yBRAAGO8FMgUQABjvBUikFFCRA1isE3ABeAGQAQGYAdgCoAH4FKoBBzAuMS4xLje4AQPIAQD4AQGYAgagApkLqAIKwgIHECMYJxjqAsICCBAAGIAEGLEDwgIFEAAYgATCAgQQABgDwgIFEC4YgATCAgsQLhiABBjHARivAZgDCfEFDn6e4GDDFDuSBwcxLjEuMS4zoAfVUbIHBzAuMS4xLjO4B48LwgcFMC4zLjPIBxeACAA&sclient=gws-wiz-serp&mstk=AUtExfCEMLR8H9MP0dbqSLGtwGyBpn9-Z8nHYyT8FLFAK6cwRxCmUdwCsfV4nXL1FNM8gVVCXWrLxYAvwy7TRfdumxEsK5JT8Y8u0N-BXVSD6LrS453XMH1HNdZndmYKU9w6sINiSuuat_AU5WKhoA5zyx0OnIxcwLwS8vFuI8YbByikHac&csui=3) **(shénqí, 선치**
**我想问你一个问题。** (Wǒ xiǎng wèn nǐ yíge wèntí. / 워 시앙 원 니 이거 원티)
化妆品 huàzhuāngpǐn 화장품
等一下děng yīxià
女生 nǚshēng
太好了tài hǎo le


daizi, 봉투 (다이즈)
caidan 메뉴판 (차이단)
zhe ge 이거 (저거)

keyi gei wo caidan ma ?


~ 주실 수 있나요  ? 
- keyi gei wo shui ma ?


1.kubernetes practice 



  Playwright MCP 테스트는 크게 두 가지로 나뉩니다:                                                                                                                                                                                                                                                                       
  1. Happy Path - 정상 흐름 검증 (탭 클릭 → 데이터 조회 → 렌더링)
  2. Regression - 기존 탭(나의일정, 연간일정 등)이 영향받지 않았는지 확인 



**买单 (mǎidān / 마이딴):** 식당에서 **"계산할게요(계산서 주세요)"**라고 말할 때 가장 많이 쓰는 표현입니다.
- mǎidān, qǐng. / **마이딴, 칭.**)
- 물건을 달라고 할 땐: **"给(게이) + 물건"**
- 행동을 부탁할 땐: **"커이(可以) + 행동"** 또는 **"행동 + 칭(请)"**

**请等一下。"** (qǐng děng yīxià / **칭 덩 이샤**)  , 잠시만 기다려주세요
太好了tài hǎole



---

~ 이거 주세요 : keyi gei wo (명사) ma?

**还没呢。** (Hái méi ne.) , 아직 없어
太棒了 (Tài bàng le) - "멋지다!"
太好了 (Tài hǎo le) - "좋다!"
明天吧 (Míngtiān ba) - 내일 어때? / 내일 하자.
我随时都有空 (Wǒ suíshí dōu yǒu kòng), 나 **언제든지** 시간 있어.
	你想吃什么? (Nǐ xiǎng chī shénme?) - 너 뭐 먹고 싶어?
随便 (Suíbiàn) - 아무거나 / 상관없어.

Míngtiān 내일 
ba ~ 하자
xiǎng 원하다
chī 먹다
Suíbiàn 아무거나 
**随 (suí):** 따르다
**时 (shí):** 때, 시간
**有 (yǒu):** '있다'
**都 (dōu) ** : **다(모두)**
**空 (kòng):** '틈, 여유, 빈 시간'이라는

sao ba
jiran shuo le hui dasao
na jiu kuai dongshou a
shuo shenme bu zhongyao
zuo shenme cai zhongyao
sao

**你用过这个吗？** (Nǐ yòng guò zhège ma?) - 너 이거 써본적있어?

**没关系 (méi guān xi - 메이 꽌 시):** "괜찮다", "상관없다"는 뜻으로, 사과(미안해)를 받았을 때 답으로 주로 씁니다.
**别担心 (bié dān xīn - 비에 딴 신):** "걱정하지 마"라는 의미로 상대방을 안심시킬 때 씁니다.

小鱼很关注皮肤护理吗 ？ xiaoyu hen guan zhu pifu huli ma

关注 (guānzhù): 주의를 기울이거나 관심을 두는 것을 말합니다.
皮肤护理 (pífū hùlǐ): '피부(皮肤)' + '관리/케어(护理)'가 합쳐진 단어입니다.

**你在听什么呢？** (Nǐ zài tīng shénme ne?)
- **의미:** 너 지금 뭐 듣고 있어
- **팁:** '在(zài)'와 '呢(ne)'를 붙이면 **"지금 ~하고 있니?"**라는 진행형 질문이 되어 가장 자연스럽습니다.

**韩国男生好像也很注重皮肤保养。”** (Hánguó nánshēng hǎoxiàng yě hěn zhùzhòng pífū bǎoyǎng.)

ting , 듣다
**주중(注重, zhùzhòng):** '중시하다'
**보양(保养, bǎoyǎng):** '관리/보양하다' (피부나 건강을 관리할 때 자주 쓰는 단어)

**小鱼，我打算在中国待10天左右，其中成都大概待3到4天。** (Xiǎoyú, wǒ dǎsuàn zài Zhōngguó dāi 10 tiān zuǒyòu, qízhōng Chéngdū dàgài dāi 3 dào 4 tiān.)

- **打算 (dǎsuàn):** ~할 계획이다.
- **左右 (zuǒyòu):** ~정도(쯤).
- **独自旅行 (dúzì lǚxíng):** 혼자 여행하다.
- **片区域 (piàn qūyù):** '구역/지역'을 뜻하며, 위치를 물을 때 아주 자연스러운 표현입니다.

**太长了！** (Tài cháng le!)
**记住啦 (jìzhù la)**는 한국어로 **"기억했어!"**, **"기억했어!"** 또는 **"다 외웠어!"**라는 뜻입니다.

----

**好可爱呀！** (Hǎo kě'ài ya!)
- **해석:** (정말/너무) 귀엽네~

**我不太清楚。** (Wǒ bù tài qīngchu.)

**“太厉害了，现在是韩语的完全开始啊。”**

- **직역:** "정말 대단해, 지금은 한국어의 완전한 시작이네."
- **의미:** "정말 대단하다, 이제야말로 한국어를 본격적으로 시작하는구나!" (상대방이 한국어를 본격적으로 배우기 시작했거나, 실력이 크게 늘었음을 칭찬할 때 쓰는 표현입니다.)

---

### 2. 단어 뜻

- **太 (tài):** 너무, 정말
- **厉害 (lìhai):** 대단하다, 훌륭하다, 무섭다(실력이 좋을 때 쓰는 감탄사)
- **了 (le):** (문장 끝에 붙어) 변화나 상태의 지속을 나타냄
- **现在 (xiànzài):** 지금, 이제
- **是 (shì):** ~이다
- **韩语 (Hányǔ):** 한국어
- **的 (de):** ~의 (관형격 조사)
- **完全 (wánquán):** 완전한, 완전히
- **开始 (kāishǐ):** 시작, 시작하다


**好啦。** (Hǎo la.) : **의미:** 그래, 알겠어~

- **사랑: 爱 (ài)**
- **행복: 幸福 (xìngfú)**
- **노력: 努力 (nǔlì)**
- **예쁘다: 漂亮 (piàoliang)**

这些 (zhèxiē)

**"샤오위, 잘했어!"**

> **"小鱼，做得好！"** (Xiǎoyú, zuò de hǎo!)

**"와, 진짜 잘했다!"**

> **"哇，太棒了！"** (Wā, tài bàng le!)

**这次我是独自旅行，你能不能给我推荐一下住在哪片区域比较好？** (Zhè cì wǒ shì dúzì lǚxíng, nǐ néng bù néng gěi wǒ tuījiàn yīxià zhù zài nǎ piàn qūyù bǐjiào hǎo?)


**"这几个容易忘记怎么拼。"**

- **의미:** "이것들은 어떻게 쓰는지(철자를) 자꾸 잊어버리게 돼."

---

### 2. 단어 뜻

- **这几个 (zhè xiě ge):** 이것들 / 이 몇 가지들
- **容易 (róngyì):** 쉽다 (뒤에 '잊어버리기 쉽다'처럼 쓰여 ~하기 쉽다는 의미로 사용)
- **忘记 (wàngjì):** 잊어버리다 / 까먹다
- **怎么 (zěnme):** 어떻게
- **拼 (pīn):** (단어의) 철자를 쓰다 / 철자를 맞추다 / (병음을) 조합하다


**发音是一样的。** (Fāyīn shì yīyàng de.)

- **의미:** 발음은 똑같아.


**我要去睡觉了。** (Wǒ yào qù shuìjiào le.)


### 2. 단어 뜻

- **成都 (Chéngdū):** 청두 (중국 사천성의 성도)
- **交通 (jiāotōng):** 교통
- **比较 (bǐjiào):** 비교적, 꽤
- **方便 (fāngbiàn):** 편리하다
- **住 (zhù):** 머무르다, 살다, 숙박하다
- **哪里 (nǎlǐ):** 어디(든)
- **都 (dōu):** 모두, 다
- **挺好的 (tǐng hǎo de):** 꽤 괜찮다, 아주 좋다


**看你想去哪个地方玩儿，其实都可以。二环以内价格可能会贵一点。如果在网上订的话，价格其实差不了多少。”**

- **의미:** "네가 어디를 구경하러 가고 싶은지에 따라 달라, 사실 어디든 다 괜찮아. 2환(이환) 안쪽은 가격이 조금 비쌀 수도 있어. 만약 인터넷으로 예약한다면, 가격은 사실 크게 차이 나지 않아."
    

---

### 2. 단어 뜻

- **看 (kàn):** ~에 따라 다르다, (~를) 보다
- **想去 (xiǎng qù):** 가고 싶다
- **哪个地方 (nǎge dìfāng):** 어느 곳 / 어느 지역
- **玩儿 (wánr):** 놀다, 여행하다, 구경하다
- **其实 (qíshí):** 사실, 실제로는
- **都可以 (dōu kěyǐ):** 다 괜찮다, 무엇이든 가능하다
- **二环以内 (èrhuán yǐnèi):** 2환 안쪽 (중국 도시들은 도로를 원형으로 감싸는 '환'으로 구역을 나눕니다. 2환 안이면 중심가를 뜻합니다.)
- **价格 (jiàgé):** 가격
- **可能会 (kěnéng huì):** ~할 수도 있다
- **贵一点 (guì yīdiǎn):** 조금 비싸다
- **如果在...的话 (rúguǒ zài... de huà):** 만약 ~한다면
- **网上订 (wǎngshàng dìng):** 인터넷으로 예약하다
- **差不了多少 (chà bù liǎo duōshǎo):** 별로 차이 나지 않다 (차이가 크지 않다)

---

**Software Product Line (SPL) Architecture**.

In this setup:

- **Core:** The "System of Record" or Infrastructure layer.
- **Platform:** The "Kernel" or Domain layer (common business logic).
- **Customer X:** The "Tenant-specific" or "Feature" layer.


stateless - core 
stateful - platform 


샤오위가 토요일이랑 일요일에 편하다고 했지?" (상대방에게 되물어볼 때)

- **小鱼说过周六和周日方便吧？**
- (Xiǎoyú shuōguò zhōuliù hé zhōurì fāngbiàn ba

- 여행 계획 짜는 데 필요해서 물어본 거야, 고마워!"
- **因为在做旅行计划，所以问了一下，谢谢！**
- (Yīnwèi zài zuò lǚxíng jìhuà, suǒyǐ wènle yīxià, xièxie!)

- tai bang le 
- tai hao le 


- os 재설치, 동일하게 
- nexus backup 70GB, backup solution exsits, but it is not good choice

---

tài bàng le : 최고다(칭찬)
tài hǎo le : 좋다(감탄)

méi guān xi : 괜찮아 (사과를 받는경우)
méishì : 아무 일도 아냐
méishénme : 별거 아냐 

Hǎo fùzá ya : 복잡하네. 
- fùzá : 복잡하다
- ya : 문장끝에서 말을 부드럽게 한다.



nǐ hěn néng chī là ma? : 너 매운 거 잘 먹니 ? (니 헌 넝 치 라 마?)
- **hěn / 헌):** 아주
- **néng / 넝):** ~할 수 있다
- bùnéng, 뿌넝): ~ 할 수 없다

wǒ huì shuō zhōngwén 
- shuō, 슈오 말하다 

### 조금

(yīdiǎnr / 이디알) : 조금
(hěn / 헌) : 많이
(zhēn / 쩐) : 진짜 
(fēicháng / 페이창) : 엄청 / 매우
(tài le, 타이러) : 매우 



### 날짜 
---

**(jīntiān / 찐티엔) :** 오늘
**(míngtiān / 밍티엔) :** 내일
**(zuótiān / 주오티엔) :** 어제
(xiànzài, 씨엔 짜이) : 지금  

**(xīngqī / 싱치) :** 주
**(yuè / 위에) :** 달
**(tiān / 티엔) :** 일
(diǎn) : 시간

**(yī gè xīngqī / 이 거 싱치) :** 한 개의 주
**(yī gè yuè / 이 거 위에) :** 한 개의 달


###  상태
---

**(bǎo / 바오) :** 배부르다


### 동사
---

#### 가다/오다

**(qù, 취):** 가다
(lái / 라이) : 오다

**(hēshuǐ, 허슈이):** 물을 마시다
(shuō,슈오) : 말하다
(guò, 꿔) : 지내다
(děng, 덩) : 기다리다

#### 알다 / 모르다 

(zhīdào, 쯔다오) : 알다 
(bù zhīdào) : 모르다 

(zuò, 쭤) : 하다 / 만들다 / 작성하다 만능단어
(shíhou, 스허우) : 시간, 때
(shénme shíhou, 션머 스허우) : 언제
（zěnmeyàng?) ： 어떄 ?

#### 자다/일어나다 

(shuìjiào, 슈이-짜오) : 잠을 자다. 
**(qǐchuáng, 치추앙):** 일어나다.

(qǐchuáng, 치-츄앙) : 일어 나다 
(pāi, 파이) : 찍다
(zhàopiàn, 쨔오뎬) : 사진 
(kàn, 칸) : 보다 
(dào) : ~까지, 도착하다
(xuéxí, 쉬에 시) : 공부하다.
(kànshū, 칸 슈) : 책을 보다.
(yào, 야오) : ~하려고 하다 (의지)

#### 출근/퇴근

(shàngbān, 샹 빤) : 출근하다.
(xiàbān, 시아빤) : 퇴근하다.

**(xiūxi, 시우시):** 쉬다.


### Example Sentence 

(shénme shíhou qù? , 션머 스허우 취?) : 언제가니 ?
(shàng yī cì, 샹 이츠): 저번
(Xièxiè nǐ xiǎng dào wǒ) : 내 생각해줘서 고마워
(Duōkuī le nǐ, 뚜오쿠이 러 니) ： 너 덕분에
(Wǒ yào qù shuìjiào le, 워 야오 취 쉐이쨔오 러) : 나 이제 잔다  

#### 나 ~ 할거야 / 나 ~ 했어 

(Wǒ yào, 워 야오) : **Wǒ yào shuìjiào**
(Wǒ ~ le, 워 ~ 러) : Wǒ chīfàn le



### 명사
---

(qūbié, 취비에) : 차이
(tiān qì, 티엔-치) : 날씨
(gōngzuò, 공-쭈어) : 일, 일하다
(fàn) : 밥, 식사
(shuǐ, 슈이) : 물
(jǐdiǎn, 찌 띠엔) :  몇 시  
(jiā, 지아)

### Example Sentence 

**(zuò gōngzuò):** 일을 하다.
(yīdiǎn dào liǎngdiǎn, 이 띠엔 따오 리앙 띠엔): 1시에서 2시까지
（shí yī diǎn dào shí èr diǎ，스 이 뎬 따오 스 얼 뎬）
(Nàbiān, 나비엔) : 그쪽 


### 조사
---

(shàng, 샹) : 지난 / 이전의

### VS 
---

néng, huì

wǒ huì shuō zhōngwén : 중국어를 배워서 할 수 있다.
wǒ néng shuō zhōngwén : 중국어를 할 수 있는 환경이다.
Wǒ yě zhème juéde! (워 예 저머 쥐에더!) 

我会说中文异地哪人

---

你很能吃辣吗？ (Nǐ hěn néng chī là ma?)

(Hǎojiǔ bùjiàn!, 하오지우 부지엔) : 오랜만이야
（Nǐ xiǎng chī zhège ma?） ：너 이거 먹고싶어?
(Shénme shíhou, 션머 스허우) : 언제
(Nǐ kàn nàge, 니 칸 나거) : 저거 봐봐

(nàge): 저것 / 그거
(zhège): 이것 / 이거

(Zǎofàn, 짜오판) : 아침
(Wǔfàn, 우판) : 점심
(Wǎnfàn, 완판) : 저녁

(jīchǎng, 지창) : 공항
(chūzūchē, 츠쭈처) : 택시
(gōngjiāochē, 꽁지아오처) : 버스
(dìtiě, 띠티에) : 지하철
(jiǔdiàn, 지우띠엔) : 호텔
(gōngsī, 꽁쓰) : 회사
(huǒchēzhàn, 후오처짠) : 기차역

(yùndòng, 윈똥) : 운동
(gǎnjué, 깐쥐에) : 느낌
(lèi, 레이) : 피곤하다
(yǒu yìsi, 요우 이쓰) : 재밌다
(xǐhuān, 시환) : 좋아하다.


**(jiùshì, 찌우쓰)** : 맞아 / 바로 그거야
**(juéde, 쥐에더)** : 생각하다 / 느끼다
(yě, 예) : ~도 / 역시
(zhème, 저머) : 이렇게 / 이만큼
**(xīnqíng, 씬칭)** : 기분
**(gānjìng, 간징)** : 깨끗하다
**(shūfu, 슈후)** : 편안하다 / 개운하다
**(duì, 뛔이)** : 맞다 / 옳다
**(jiāwù, 찌아우)** : 집안일
**(bù lèi, 뿌 레이)** : 피곤하지 않다 / 힘들지 않다

(Yìqǐ, 이치) : 같이 
(wèishénme, 웨이 션 머) ： 왜 ?


작업계획서 수정
- 작업 내용 수정 (GPU 할당 관련)
- 작업자에 이건우대리제거, 구도형 책임님께 메일로 전달
- was 가 외장톰캣이 필요한 이유

---

학습어플 - duolingo 



tianqi - 날씨 
예약  
돕다.


~ 할 수 있어 ?
~ ni yao ㅇ약마 ?



---


Wǒ lái gōngzuò le, 나 일 하러 왔어
Zhēn dā, 진짜?
Hái méi ne, 아직 아니야 
Áoyèle, kùn, 늦게까지 깨어 있었더니 졸려요.
Nǐ shénme shíhòu shuìzhe de? 

**나도 그래 / 나도 마찬가지야:**

> **我也是。** (Wǒ yě shì.) 


我明白


你不是说附近有个很漂亮的地方吗？


Wǒ gāi zěnme dào zhèlǐ?

有点难 Yǒudiǎn nán

你曾经去过那里吗？
你在干什么 ？

Wǒ zài kàn hányǔ chángyòng cíhuì

Shì yīyàng de. 똑같다
Wǒ gàosù nǐ! 내가 알려줄게 
Wǒ yǒu gè wèntí. 나 질문있어
Nǐ yǒu duō gāo? , 키가 몇이야? 
你为什么好奇这个问题

---

나만의 서비스를 만드는 것이 너무 막막하다면, **"내가 여행 유튜버를 할 때 가장 귀찮을 것 같은 일"**을 해결해 주는 프로그램을 먼저 상상해 보세요.

예를 들어, "수백 개의 영상 소스 중에서 특정 키워드가 나온 부분만 AI로 찾아주는 툴"이나 "내가 간 경로를 지도로 자동 생성해 주는 기능" 같은 것들이죠. 내가 필요해서 만든 게 의외로 남들에게도 절실할 수 있습니다.

혹시 지금 머릿속에 **"이런 거 만들면 좋겠다"** 하고 스쳐 지나간 아이디어가 하나라도 있나요? 그게 기술적으로 구현 가능한지, 혹은 시장성이 있을지 같이 브레인스토밍해 볼까요?






Uptime Kuma + Webhook
Azure & Kubernetes 경험

**OPIc:** IH (Intermediate High) 정도x`



| **단어 (한자/병음)**   | **뜻**                  |
| ---------------- | ---------------------- |
| **吃 (chī)**      | 먹다                     |
| **完 (wán)**      | 완료하다, 다 끝나다            |
| **饭 (fàn)**      | 밥, 식사                  |
| **联系 (liánxì)**  | 연락하다                   |
| **我 (wǒ)**       | 나, 저                   |
| **告诉 (gàosu)**   | 알리다, 말해주다              |
| **一声 (yìshēng)** | (짧게) 한마디, 소리 한 번       |
| **回 (huí)**      | 돌아오다, 답장하다             |
| **一下 (yíxià)**   | (동사 뒤에 붙어) 잠시, 한 번 ~하다 |