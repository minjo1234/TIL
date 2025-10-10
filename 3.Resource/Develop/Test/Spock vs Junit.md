

### Spock vs Junit 

Stub  - 기본적인 Mock 객체

| 구분        | JUnit                        | Spock                   |
| --------- | ---------------------------- | ----------------------- |
| 언어        | Java                         | Groovy                  |
| 구조        | @Test 어노테이션                  | def "test name"()       |
| 블록        | Given-When-Then 수동           | given:, when:, then: 블록 |
| Assertion | assertEquals(), assertTrue() | ==, !=, 자연스러운 표현        |
| Mock      | Mockito, EasyMock            | 내장 Mock/Stub/Spy        |
| 파라미터 테스트  | @ParameterizedTest           | where: 블록               |
|           |                              |                         |
#### JUnit 장점

- ✅ 표준: Java 생태계의 표준
- ✅ IDE 지원: 모든 IDE에서 완벽 지원
- ✅ 학습 곡선: Java 개발자에게 친숙
- ✅ 성숙도: 오랜 기간 검증됨
#### JUnit 단점

- ❌ 보일러플레이트: 많은 어노테이션과 설정
- ❌ Mock 설정: Mockito 등 외부 라이브러리 필요
- ❌ 가독성: Given-When-Then 구조가 명확하지 않음

---

#### Spock 장점

- ✅ 가독성: Given-When-Then 구조가 명확
- ✅ 내장 Mock: Mock/Stub/Spy 내장
- ✅ 파라미터 테스트: where: 블록으로 간단
- ✅ 자연스러운 Assertion: ==, != 등 직관적
- ✅ 보일러플레이트 최소화: 어노테이션 최소화

#### Spock 단점

- ❌ Groovy 의존성: Groovy 언어 학습 필요
- ❌ IDE 지원: IntelliJ는 좋지만 Eclipse는 제한적
- ❌ 성숙도: JUnit 대비 상대적으로 새로운 기술

#### Mock을 사용해야 하는 경우

- 상호작용 검증이 필요할 때
- 메서드 호출 횟수를 확인하고 싶을 때
- 특정 메서드가 호출되었는지 확인하고 싶을 때

#### Stub을 사용해야 하는 경우

- 단순히 반환값만 설정하고 싶을 때
- 상호작용 검증이 불필요할 때
- 의존성 주입만 목적으로 할 때

### 왜 Mock을 사용하는가?

#### 1. readonly property 우회

- 실제 객체: expired 필드가 readonly라서 직접 설정 불가
- Mock 객체: isExpired() 메서드의 반환값을 자유롭게 설정

MOCK 

### Mock 객체의 동작 방식


Mock 객체는:

- 객체는 생성되지만 모든 메서드가 기본값을 반환
- 내가 직접 설정한 값만 반환
- 설정하지 않은 메서드는 기본값 반환
- 값을 설정해야하는 데이터는 실제객체로 만들어서 사용하.