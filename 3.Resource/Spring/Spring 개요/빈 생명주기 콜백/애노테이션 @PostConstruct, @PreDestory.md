

InitializingBean, DisposableBean 대신에
`@PostConstruct` , `@PreDestory` 어노테이션을 사용할 수 있습니다.

#### @PostConstruct, @PreDestory 애노테이션 특징

- 최신 스프링에서 가장 권장하는 방법이다.
- 애노테이션 하나만 붙이면 된다.
- javax.annotation.PostConstruct 스프링에 종속적인게 아니라 자바 표준 기술이다.
- 컴포넌트 스캔과 잘 어울린다.