**Present project implementation method** 
- Guava EventBus Library 

**composition** 
- Producer - `AbstractEventProducer`
- Broker - `DefaultEventBroker` - `AbstractEventBroker`
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

### EventProducer (이벤트 발행)


**structure** 

> AbstractEventProducer
> 구현체Producer
   

---
