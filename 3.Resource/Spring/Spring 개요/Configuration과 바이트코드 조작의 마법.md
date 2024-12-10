스프링 컨테이너는 싱글톤 레지스토리다. 스프링이 자바 코드까지 어떻게 하기는 어렵다.
스프링의 클래스는 바이트코드를 조작하는 라이브러리를 사용한다.
모든 비밀은 `@Configuration`을 적용한 `AppConfig`에 있다.

```java
@Test
void configurationDeep() {
	ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);

	//AppConfig
	AppConfig bena = ac.getBean(AppConfig.class);

	System.out.pritnln("been = " + bean.getClass());
}
```


AppConfig가 Bean으로 등록되면 AppConfig 자체가 등록된게 아니라 CGLIP이라는 바이트코드 조작 라이브러리를 사용하여 AppConfig를 상속받은 임의의 다른 클래스를 만들고, 그 다른 클래스를 스프링 빈으로 등록
-> 해당 클래스가 싱글톤으로 조작되도록 설정해준다.

---

`AppConfig@CGLIP 예상코드`

```java
@Bean
public MemberRepository memberRepository() {

	if(memoryMemberRepository) { // 이미 스프링 컨테이너에 등록되어 있으면
		return 스프링 컨테이너에서 찾아서 봔환 
	} else {
		return 반환
	}
}
```

- CGLIP에 상속된 코드를 이용하여 반환이 정상적으로 완료되는 것이다.
- AppConfig@CGLIP은 AppConfig의 자식이기 때문에 AppConfig를 조회할 수 있는 것이다.

---

@Configuration을 사용하지않고 @Bean을 등록하게 될 경우에는 
싱글톤을 보장받지 못한다.
- @Bean만 사용해도 스프링 빈으로 등록되지만, 싱글톤을 보장하지 않는다.
  
---
@Component를 사용하게 되면 

의존관계설정을 어떻게 할지에 대해서

```java
public MemberServiceImpl(MemoryRepository memoryRepository)
```