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

참고: [[모놀리식 VS 마이크로 서비스]]


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

생각한 점 

> “현재 프로젝트는 모놀리식 구조라 이벤트가 모두 JVM 내부에서만 오가고 있었습니다.
> 그래서 별도의 메시지 브로커(RabbitMQ)를 운영하는 건 오버엔지니어링이라 판단했고,
> Guava EventBus를 도입해 가볍게 이벤트 기반 구조를 구현했습니다.
> 다만 향후 마이크로서비스로 확장 시에는 RabbitMQ나 Kafka 같은 브로커 도입도 고려할 수 있습니다.”


### MQ

```
// Message Queue = 메시지 큐
// 애플리케이션 간 비동기 통신을 위한 중간 저장소
// 메시지를 임시로 저장하고 전달하는 시스템

// FIFO (First In, First Out) 구조
// 먼저 들어온 메시지가 먼저 처리됨
// 은행 대기줄과 같은 개념
```

---

### EventBus vs AsyncEventBus 차이

| **구분** | **EventBus**                                           | **AsyncEventBus**                        |
| ------ | ------------------------------------------------------ | ---------------------------------------- |
| 실행 방식  | **동기** (Producer가 이벤트 발행하면, Consumer가 즉시 같은 스레드에서 실행)  | **비동기** (스레드 풀에 위임 → 별도 스레드에서 실행)        |
| 특징     | 간단, 순차적, 예측 가능 (단점: Consumer 처리 시간이 길면 Producer도 블로킹됨) | 고성능, 병렬 처리 가능 (단점: 순서 보장 어려움, 스레드 관리 필요) |
| 사용 예시  | 이벤트 수가 적고, Consumer 처리 시간이 짧은 경우                       | Consumer가 오래 걸리거나, 이벤트가 빈번하게 발생하는 경우     |

---
EventChannel 

- evnetKey, async 를 만들어 확장성 고려 
- 서비스 로직(단일 트랜잭션)
- EventBus(다중 트랜잭션)
	- Consumer 비동기로 작동 
	- EventAuditor 다른 트랜잭션


ThreadPoolTaskExecutor
