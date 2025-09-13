- Observer Pattern: EventBus → @Subscribe 리스너들

```
// Producer에서 이벤트 발행
producer.produce(createAppEvent);
↓
// EventBus.post() 호출
eventBus.post(createAppEvent);
↓
// Guava EventBus가 자동으로 @Subscribe 메서드 탐지
// 매칭되는 Consumer의 consume() 메서드 자동 호출
```

- Publisher-Subscriber Pattern: Producer → EventBus → Consumer

```

```

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

---
### EventProducer (이벤트 발행)


**structure** 

> AbstractEventProducer
> 구현체Producer

---

**overall action flow** 

```
1. Producer.produce(event)
   ↓
2. EventChannel.sendEvent(event)
   ↓
3. EventBus.post(event) + EventWatcher.eventSent(event)
   ↓
4. @Subscribe → Consumer.consume(event)
   ↓
5. EventAuditor → 감사 로그 저장 + 알람 발송
```

---

**EventChannel을 공유한다.**

1. Consumer 생성 시: EventChannel 생성 및 Consumer 등록
2. Producer 생성 시: 기존 EventChannel 조회 및 참조 획득

---



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




Event(met)





----


- plugin Architecture 
- 