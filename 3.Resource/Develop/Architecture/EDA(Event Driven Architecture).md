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

- Publisher-Subscriber Pattern: Producer → EventBus(EventListener) → Consumer

```
EventListener - EventConsumer(API용도 복잡한 로직은 Takser) EventTasker  
EventWatcher -EventAuditor(감사 로그)
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

---

**이렇게 구현한 이유**

단일 어플리케이션 아키텍쳐 

```
// 마이크로서비스가 아닌 모놀리식 구조
// 모든 이벤트가 같은 JVM 내에서 처리
```



```txt


// 마이크로서비스가 아닌 모놀리식 구조
// 모든 이벤트가 같은 JVM 내에서 처리

```

- 모놀리식 구조 (RebbitMQ나 Kafka등을 사용하지 않음.)


```
// 여러 애플리케이션 간 통신
// 마이크로서비스 아키텍처
```

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


