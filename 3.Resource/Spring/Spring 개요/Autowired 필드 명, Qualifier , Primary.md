
### @Autowired

Autowired 필드명을 입력하면 
```java

@Autowired
public OrderServiceImpl(MemberRepository demberRepository, DiscountPolicy discountPolicy){
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
																
