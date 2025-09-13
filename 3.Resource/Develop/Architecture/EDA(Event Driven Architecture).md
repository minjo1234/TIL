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

### 이렇게 구현한 이유

**단일 어플리케이션 아키텍쳐** 

```
// 마이크로서비스가 아닌 모놀리식 구조
// 모든 이벤트가 같은 JVM 내에서 처리
```

**빠른 응답성 요구** 

```
// VM 생성, 삭제 등 실시간 처리 필요
// 네트워크 지연 최소화
```

 **단순한 이벤트 처리**

```
// 복잡한 메시지 라우팅 불필요
// 단순한 Publisher-Subscriber 패턴
```


### 언제 RabbitMQ나, Kafka등이 적절한지 ? 

 **분산 시스템**

```
// 여러 애플리케이션 간 통신
// 마이크로서비스 아키텍처
```

**높은 안정성 요구**

```
// 메시지 손실 방지
// 장애 복구 필요
```

 **복잡한 라우팅**

```
// 조건부 메시지 전달
// 메시지 변환 필요
```

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


### 모놀리식 vs 