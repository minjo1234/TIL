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


