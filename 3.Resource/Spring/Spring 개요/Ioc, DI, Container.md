
### 1.Ioc(Inversion of Control)

원래는 구현객체를 생성하여 기능을 실행하고 연결하면 수행했다. 
하지만 Appconfig의 등장으로 인해서 구현 객체는 자신의 로직을 실행하는 역할만 담당한다.

기존 : OrderService -> OrderServiceImpl  ()

```
public class OrderServiceImpl 
```