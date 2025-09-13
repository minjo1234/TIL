- Observer Pattern: EventBus → @Subscribe 리스너들
- Publisher-Subscriber Pattern: Producer → EventBus → Consumer

---

**Present project implementation method** 
- Guava EventBus Library 

**composition** 
- Producer - `AbstractEventProducer` **발행만 담당**`` (eventChannel 등록)
	- 이벤트 발행자
- Broker - `DefaultEventBroker` - `AbstractEventBroker`,  **라우팅만 담당** 
	- 채널 관리자
	- 채널 관리: EvnetKey별로 독립적인 채널 생성/관리
	- 동기/비동기 처리: AsyncEventBus vs EventBus 
	- 모니터링: EventWatcher를 통한 이벤트 감시 
- Consumer  - `AbstractEventConsumer` - **처리만 담당** (consumer subcribe 설정)
- Event - `AbstractApplicationEvent`  - **데이터만 담당**
	- 이벤트에 필요한 메타데이터 포함
	- 추적 가능성 
	- 타입 안정성 
----

**add option** 
- EventWatcher(event monitoring)
- EventTasker(complex event process)
- EventAuditor  - 이벤트 감사 
- EventBus - 이벤트 전달 
- EvnetOrchestrator 


EventChannel 
EventConsumer 
EventChannel 

### EventProducer (이벤트 발행)


**structure** 

> AbstractEventProducer
> 구현체Producer


**overall action flow** 


```
1️⃣ Spring 컨테이너 시작
   ↓
2️⃣ @Component 스캔으로 Producer Bean들 발견
   ↓
3️⃣ 각 Producer Bean 생성 (의존성 주입)
   ↓
4️⃣ AbstractEventProducer 생성자 호출
   ↓
5️⃣ getChannelKey()와 isAsync() 호출
   ↓
6️⃣ EventBroker.getOrCreateEventChannel() 호출
   ↓
7️⃣ EventChannel 생성 및 등록
```

------


> 1️⃣ Producer.produce(event)
> 	↓
> 2️⃣ EventChannel.sendEvent(event)
> 	↓
> 3️⃣ DefaultEventBroker - GuavaEventChannel 
> 	 EventBus.post(event) 
> GuavaEventListener	
> 	 EvnetWatcherList.sendEvent(event)

---

EventChannel을 공유한다.

1. Consumer 생성 시: EventChannel 생성 및 Consumer 등록
2. Producer 생성 시: 기존 EventChannel 조회 및 참조 획득

---



구성 : 

```
AbstractApplicationEvent,
AbstractEventConsumer - abstract class - evnetChannel register, subscribe 
AbstractEventProducer - abstract class - isAsync()
AbstractEventBroker - 
AbstractEvent -  abstract class 
```


```
EventChannel - subscribe, unsubcribe, sendEvent, removeAll()
EventWatcher
Event
```



```
┌─────────────────────────────────────────────────────────────┐
│                    Event System Architecture                │
├─────────────────────────────────────────────────────────────┤
│  Producer Layer (발행)                                       │
│  ├─ 이벤트 생성 및 발행만 담당                               │
│  └─ 비즈니스 로직에서 이벤트 발행                            │
├─────────────────────────────────────────────────────────────┤
│  Broker Layer (관리)                                         │
│  ├─ EventChannel 생성 및 관리                               │
│  ├─ Producer/Consumer 등록 관리                             │
│  └─ 라우팅 및 연결 관리                                      │
├─────────────────────────────────────────────────────────────┤
│  EventBus Layer (전달)                                       │
│  ├─ Guava EventBus.post()                                   │
│  ├─ @Subscribe 어노테이션 처리                              │
│  └─ EventWatcher 알림                                       │
├─────────────────────────────────────────────────────────────┤
│  EventWatcher Layer (감시)                                   │
│  ├─ 모든 이벤트 모니터링                                     │
│  ├─ 필터링 및 감사 로그 저장                                 │
│  └─ 알람 발송                                                │
├─────────────────────────────────────────────────────────────┤
│  Consumer Layer (처리)                                       │
│  ├─ 실제 비즈니스 로직 수행                                  │
│  └─ 이벤트에 따른 작업 처리                                  │
└─────────────────────────────────────────────────────────────┘
```


Guaba EvnetBus 
- EventBus는 이벤트를 처리할 각 이벤트 리스너를 등록하고 각 리스너에게 이벤트를 전파하는 역할을 수행한다.


Event(met)





----


- plugin Architecture 
- 