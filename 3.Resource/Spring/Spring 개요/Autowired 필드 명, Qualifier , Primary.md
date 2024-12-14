
### @Autowired

Autowired 필드명을 입력하면 역할이 아니라 구현에 직접 의존한다.
별로 택하는 방식은 아니다 DIP를 위반하는 방식이므로..

```java

@Autowired
public OrderServiceImpl(MemberRepository demberRepository, DiscountPolicy rateDiscountPolicy){
	this.memberRepository = memberRepository;
	this.discountPolicy = rateDiscountPolicy;
}
```


### @Qualifer  

이름을 지칭할 수 있지만 명확하지 않으므로 모든 클래스에서 사용할 것이 아니라면 사용을 자제한다.

```java
@Component
@Qualifier("rateDiscountPolicy)
public class RateDiscountPolicy implements DiscountPolicy {}
```

```java
@Autowired
public class OrderServiceImpl(MemberRepository demberRepository, @Qualifier("rateDiscountPolicy) DiscountPolicy discountPolicy){
	this.memberRepository = memberRepository;
	this.discountPolicy = discountPolicy;
}```
																
---

### @Primary 

이거 좋다. primary로 지칭하면 해당 빈을 인식해서 지원해준다

```java

@Component
@Primary
public class RateDiscountPolicy implements DiscountPolicy

@Component
public class DiscountPolicy implements
DiscountPolicy
```

---

메인 데이터베이스와 서브 데이터베이스를 함께 사용하는 경우
메인 데이터베이스 : @Primary 지정
