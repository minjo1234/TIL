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

Broker : event create, publish, sub