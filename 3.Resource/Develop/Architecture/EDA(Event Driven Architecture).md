**Present project implementation method** 
- Guava EventBus Library 

**composition** 
- Producer - `AbstractEventProducer` **발행만 담당**``
	- 이벤트 발행자
- Broker - `DefaultEventBroker` - `AbstractEventBroker`,  **라우팅만 담당**
	- 채널 관리자
	- 채널 관리: EvnetKey별로 독립적인 채널 생성/관리
	- 동기/비동기 처리: AsyncEventBus vs EventBus 
	- 모니터링: EventWatcher를 통한 이벤트 감시 
- Consumer  - `AbstractEventConsumer` - **처리만 담당**
- Event - `AbstractApplicationEvent`  - **데이터만 담당**
	- 이벤트에 필요한 메타데이터 포함
	- 추적 가능성 
	- 타입 안정성 

**add option** 
- EventWatcher(event monitoring)
- EventTasker(complex event process)
- EventAuditor 
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
> 3️⃣ DefaultEventBroker -  EventBus, EvnetChannel 

---
