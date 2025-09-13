**Present project implementation method** 
- Guava EventBus Library 



**composition** 
- Producer - `AbstractEventProducer`
- Broker - `DefaultEventBroker` - `AbstractEventBroker`
- Consumer  - `AbstractEventConsumer`
- Event - `AbstractApplicationEvent`

add option 
- EventWatcher(event monitoring)
- EventTasker(complex event process)


### EventProducer (이벤트 발행)


**structure** 

> AbstractEventProducer
> 구현체Producer
   
