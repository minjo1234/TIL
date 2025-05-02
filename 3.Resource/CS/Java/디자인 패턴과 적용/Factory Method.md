
### 🌟 요점 정리

- `List<TestConnectionStrategy>`는 구현체들의 목록이 자동으로 주입됨
- 이건 Spring DI 컨테이너가 해주는 기능
- 이후 `Map<Enum, Strategy>`로 바꾸면 `Enum` 기반 라우팅이 가능해짐

---

혹시 이 전략들 중 일부만 조건부로 등록하고 싶다면 `@ConditionalOnProperty` 같은 것도 함께 쓸 수 있어요.  
이 구조로 실제 구현해보셨나요, 아니면 적용을 고민 중이신가요?

---


### ❓그럼 `WebClientFactory`는 어떤 쪽?

`WebClientFactory`는 **둘 중 어느 쪽도 100% 일치하지 않지만**,  
**구현상 Factory Method 패턴에 가까운 단순 Factory**에 해당합니다.

- `WebClientFactory`는 `WebClient`라는 **단일 제품**만 생성하며,
- 서브클래싱 없이 **파라미터(baseUrl)**에 따라 생성 방식이 다름

👉 이런 형태는 흔히 **Simple Factory** 또는 **Static Factory**라고도 부릅니다.
