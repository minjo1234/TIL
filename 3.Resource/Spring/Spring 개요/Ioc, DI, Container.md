
### 1.Ioc(Inversion of Control)

원래는 구현객체를 생성하여 기능을 실행하고 연결하면 수행했다. 
하지만 Appconfig의 등장으로 인해서 구현 객체는 자신의 로직을 실행하는 역할만 담당한다.

기존 : OrderService -> OrderServiceImpl  ()

```java
public class OrderServiceImpl implements OrderService {
		private final MemberRepository MemberRepository
		private final DisCountPolicy fixDiscountPolicy
- 이런 식으로 인터페이스의 구현객체를 직접결정하여 구현객체가 어떤 객체를 실행할 지에 대한 인식을 하였지만
}
```

```java
public OrderServiceImpl(MemberRepository memberRepository, DisCountPolicy disCountPolicy) {  
    this.memberRepository = memberRepository;  
    this.disCountPolicy = disCountPolicy;  
}

- 구현객체는 인터페이스만 호출할 뿐 어떤 구현객체가 실행될지에 대해서는 모르는 제어의 역전
```


-- 프로그램의 흐름을 직접 제어하는게 아니라 Appconfig같은 외부에서 관리한느 