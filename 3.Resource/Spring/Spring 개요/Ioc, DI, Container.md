
### 1.Ioc(Inversion of Control)

원래는 구현객체를 생성하여 기능을 실행하고 연결하면 수행했다. 
하지만 Appconfig의 등장으로 인해서 구현 객체는 자신의 로직을 실행하는 역할만 담당한다.
프로그램의 흐름을 직접 제어하는게 아니라 Appconfig같은 외부에서 관리한느 것이 제어의 역전이다.
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


### 프레임워크 vs 라이브러리

프레임워크는 해당 프레임워크의 라이프사이클이 있어서 내가 코드를 작성하더라도 해당 프레임워크의 라이프사이클에 맞춰 실행되기 때문에 제어의 역전이며,

내가 작성한 코드가 직접 제어의 흐름을 담당한다면 프레임워크가 아니라 라이브러리이다.

---

### 의존관계 주입

OrderServiceImpl은 DisCountPolicy 인터페이스에만 의존한다. 실제 어떤 구현 객체가 사용될지는 OrderServiceImpl은 알지못한다.

정적인 클래스 의존관계와 - 코드를 실행하지 않아도 알수있는 의존관계주입
`OrderServiceImpl -> DiscountPolicy, MemberRepository 의존`
동적인(실행시점의) 객체 의존 관계 둘을 분리하여 생각 -  애플리케이션 실행 시점에 외부에서 실제 구현 객체를 생성하여 클라이언트 서버의 실제 의존관계가 설정되는 것을 의존관계 주입

의존관계 주입을 사용하면 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있다.
의존관계 주입을 사용하면 정적인 클래스 의존관계를 변경하지 않고, 동적인 객체 인스턴스

