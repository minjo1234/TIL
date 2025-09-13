**Present project implementation method** 
- Guava EventBus Library 

**composition** 
- Producer - `AbstractEventProducer` 
	- 이벤트 발행자
- Broker - `DefaultEventBroker` - `AbstractEventBroker`, ``
	- 채널 관리자
	- 채널 관리: EvnetKey별로 독립적인 채널 생성/관리
	- 동기/비동기 처리: AsyncEventBus vs EventBus 
	- 모니터링: EventWatcher를 통한 이벤트 감시 
- Consumer  - `AbstractEventConsumer`
- Event - `AbstractApplicationEvent`
	- 이벤트에 필요한 메타데이터 포함
	- 추적 가능성 
	- 타입 안정성 

**add option** 
- EventWatcher(event monitoring)
- EventTasker(complex event process)
- EventAuditor 
- EvnetOrchestrator 


EventChannel 


### EventProducer (이벤트 발행)


**structure** 

> AbstractEventProducer
> 구현체Producer
   

---
