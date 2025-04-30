---
aliases:
  - Test 도구
author: Min Jo
tags:
  - Test
created: 2025-04-30
---
# Test 도구 
---
junit은 java 기반  : java 코드로 테스트 작성
groovy groovy 기반 : groovy 코드로 테스트 작성

### 🔹 다시 정리하면:

|항목|JUnit|Spock|
|---|---|---|
|**언어 기반**|**Java**|**Groovy**|
|**작성 언어**|Java 코드로 테스트 작성|Groovy 코드로 테스트 작성|
|**스타일**|전통적인 단위 테스트 스타일|BDD(Given-When-Then) 스타일|
|**호환성**|Java 프로젝트 기본 테스트 프레임워크|Groovy를 사용하는 JVM 기반 프로젝트에서 사용 가능|
|**Spring 통합**|Spring Boot에서 기본 지원|Spring Boot와도 통합 가능 (설정 필요)|

**Groovy = Java와 100% 호환되면서, 문법은 더 간단하고 유연한 JVM 언어**입니다.

---


# 내가 Junit 대신에 Spock을 선택한 이유 

## ✅ Spock의 장점 (vs JUnit)

### 1. **가독성 높은 BDD 스타일 문법**

- `given-when-then` 구조로 테스트 시나리오가 명확하게 드러납니다.
    
- 영어 문장처럼 읽혀서 비개발자도 테스트 내용을 어느 정도 이해할 수 있습니다.
    

groovy

CopyEdit

`def "사용자 로그인에 성공하면 홈으로 이동한다"() {     given:     def user = new User("test", "1234")      when:     def result = loginService.login(user)      then:     result == "home" }`

→ **JUnit에 비해 시나리오 기반 테스트 작성이 훨씬 자연스럽습니다.**

---

### 2. **데이터 기반 테스트 (Data-Driven Testing)**

- `where:` 블록을 통해 다양한 입력값을 반복 테스트할 수 있어 **매우 강력**합니다.
    

groovy

CopyEdit

`def "두 수의 최대값은 올바르게 계산된다"(int a, int b, int expected) {     expect:     Math.max(a, b) == expected      where:     a | b || expected     1 | 3 || 3     7 | 4 || 7     5 | 5 || 5 }`

→ **JUnit에서는 매번 `@ParameterizedTest`와 복잡한 어노테이션을 써야 하죠.**

---

### 3. **내장 Mocking, Stubbing, Interaction Testing**

- `Mock()`, `Stub()`, `Spy()` 등 객체를 쉽게 생성하고, **호출 횟수나 순서를 검증하는 것이 매우 직관적**입니다.
    

groovy

CopyEdit

`def "메일을 보낼 때 서비스가 호출된다"() {     given:     def mailService = Mock(MailService)     def userService = new UserService(mailService)      when:     userService.sendWelcomeMail("user@test.com")      then:     1 * mailService.send("user@test.com") // 호출 검증 }`

→ **JUnit + Mockito에 비해 코드가 훨씬 간결하고 읽기 쉽습니다.**

---

### 4. **Groovy의 간결한 문법을 그대로 사용**

- 리스트/맵 선언, 문자열 처리, null-safe 연산자 등 Java보다 문법이 간단하고 유연합니다.
    

---

### 5. **JUnit과 함께 사용 가능**

- JUnit 기반 테스트와 Spock 테스트를 **동시에 프로젝트에 넣어도 문제없습니다.** Gradle이나 Maven에서 설정만 잘 해주면 됩니다.
    

---

## ❗️단점도 존재합니다

- **Groovy 기반**이기 때문에 프로젝트에 Groovy 설정이 필요함
    
- 팀원이 Groovy 문법에 익숙하지 않으면 진입 장벽이 있을 수 있음
    
- 일부 Spring 테스트 기능이 JUnit 위주로 먼저 지원되는 경우가 있음
    

---

## 🔚 결론

Spock은 특히 **복잡한 비즈니스 로직을 테스트하거나, 데이터 조합 테스트가 많은 경우**, 그리고 **Mocking이 많이 필요한 서비스 레이어 테스트**에서 빛을 발합니다.

---

어떤 타입의 테스트에 Spock을 주로 쓰고 계신가요? (예: 서비스, 컨트롤러, 리포지토리 등)

@Controller 