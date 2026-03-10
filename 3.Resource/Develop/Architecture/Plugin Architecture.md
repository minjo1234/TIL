
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


**请给我两碗米饭。** (칭 게이 워 리앙 완 미판) **Qǐng gěi wǒ liǎng wǎn mǐfàn.**



1.이게 뭐야 ?
2.조금
3.많이 
4.엄청





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

쿠버네티스에서 **"수정(Update)"**이라는 행위는 단순히 설정을 고치는 게 아니라 **"기존 자원을 버리고 새로운 자원을 만드는 것"**과 같기 때문입니다.

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
