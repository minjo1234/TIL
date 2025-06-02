### Define :  Configure systems that generate, transmit, and react to events 

---
### Component : 

- Event Producer 
	- create event and occur 
	- example user clicks the button then make the click event 
- Event Broker 
	- transmit event, management role
- Event Consumer 
	- Subscribe event and process event 
	- when an event occur, receive it and perform an action 

----
###  Feature 
- Asynchronous processing 
	- After the event is created, it is not processed immediately, event consumer process asynchronous 
- flexibility and scalability 
	- new event producer and consumer append easily, so scalability useful 
- loose coupling 
	- producer does not connect consumer directly, so connect indirectly through event broker 


----

### Example 

Broker : event  , publish, subscribe 
Producer : event create, publish through broker
Consumer : process event that registered event broker 


Exception thrown by subscriber method handle(com.clovircm.eventbus.ApplicationEvent) on subscriber com.clovircm.eventbus.DefaultEventBroker$GuavaEventListener@37a5715d when dispatching event: com.clovircm.application.aria.vm.power.AriaVmPowerEvent@4ad08f3c 

VM.ShutdownGuest


[2025.06.02 13:15:09.381] [http-nio-8086-exec-6] | -WARN  64170 --- c.c.m.DatabaseMessageSource : ### 메세지 code를 찾을 수 없습니다. code : btn_close, locale : ko 

1
2
