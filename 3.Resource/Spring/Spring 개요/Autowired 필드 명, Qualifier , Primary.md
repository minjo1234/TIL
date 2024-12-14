

```java

@Autowired
public OrderServiceImpl(MemberRepository demberRepository, DiscountPolicy discountPolicy){
	this.memberRepository = memberRepository;
	this.discountPolicy = rateDiscountPolicy;
}
```


### @Qualifer  - 

```java

@Autowired
public OrderServiceImpl(MemberRepository demberRepository, @Qualifier("rateDiscountPolicy) DiscountPolicy discountPolicy){
	this.memberRepository = memberRepository;
	this.discountPolicy = discountPolicy;
}

