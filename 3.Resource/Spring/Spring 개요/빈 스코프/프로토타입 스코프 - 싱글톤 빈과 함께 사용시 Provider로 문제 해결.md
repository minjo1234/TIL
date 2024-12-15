
#### ObjetFactory, ObjectProvider

지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공하는 것이 바로 `ObjectProvider` 참고로 과거에는 `ObjectFactory`가 있었는데, 편의 기능을 추가해서 `ObjectProvider`가 만들어졌다.

---

- ObjectFactory : 기능이 단순, 별도의 라이브러리 필요 없음, 스프링에 의존
- ObjectProvider : ObjectFactory 상속, 옵션, 스트림 처리등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존

---

### JSR-330 Provider

마지막 방법은 `javax.inject.Provider` 라는 JSR-330 자바 표준을 사용하는 방법이다.
이 방법을 사용하려면 `javax.inject:javax.inject:1` 라이브러리를 gradle에 추가해야 한다.

---

그런데 실무에서 프로토타입으로 개발할 일이 거의없다.

```text
A -> B 
B -> A 를 의존하는 순환참조에 경우에는, 참조하는 경우에
			항상 참조하지 않는다면, 프로토타입을 이용한다.
		@LookUp 어노테이션을 사용하는 경우도 많이 존재한다.
	
```

### 참조

실무에서 자바 표준인 JSR 330 Provider를 사용할 것인지, 아니면 스프링이 제공하는 ObjectProvider를 사용할 것인지 고민이 될 것이다.
ObjectProvider는 DL을 위한 편위 기능을 많이 제공해주고