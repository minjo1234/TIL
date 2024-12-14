

```java

@Autowired
public OrderServiceImpl(MemberRepository demberRepository, DiscountPolicy discountPolicy){
	this.memberRepository = memberRepository;
	this.discountPolicy = discountPolicy;

}

```