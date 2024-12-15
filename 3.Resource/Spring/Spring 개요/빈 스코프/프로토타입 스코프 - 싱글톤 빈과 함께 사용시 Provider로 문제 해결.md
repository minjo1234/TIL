
#### ObjetFactory, ObjectProvider

지정한 빈을 컨테이너에서 대신 찾아주는 DL 서비스를 제공하는 것이 바로 `ObjectProvider` 참고로 과거에는 `ObjectFactory`가 있었는데, 편의 기능을 추가해서 `ObjectProvider`가 만들어졌다.

---

- ObjectFactory : 기능이 단순, 별도의 라이브러리 필요 없음, 스프링에 의존
- ObjectProvider : ObjectFactory 상속, 옵션, 스트림 처리등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존

---

### JSR-330 Provider

마지막 방법은 `javax.inject.Provider` 라는 JSR-330 자바 표준을 사용하는 방법이다.
이 방법을 사용하려면 `javax.inject:javax.inject:1` 라이브러리를 gradle에 추가