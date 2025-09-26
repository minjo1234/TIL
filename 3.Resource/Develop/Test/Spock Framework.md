
### Spock Framework 

### 1.Mock 
- 의존성 검증: 메서드가 호출되었는지 확인
- 호출 횟수 검증: 몇 번 호출되었는지 확인
- 매개변수 검증: 어떤 값으로 호출되었는지 확인

### 2.Stub

- 반환값만 설정: 호출 검증은 필요 없고 값만 필요할 때
- 의존성 대체: 실제 객체 대신 가짜 객체로 동작하게 할 때
- 테스트 데이터 제공: 미리 정의된 데이터 반환

### 3.Spy (스파이 객체)

- 부분적 Mock: 실제 객체의 일부 메서드만 Mock으로 동작
- 실제 로직 + Mock: 대부분은 실제 동작, 특정 부분만 Mock
- 기존 객체 감시: 이미 생성된 객체를 감시하고 싶을 때

---

Spock vs Junit 

Junit은 TDD 기반  - 테스트 자체에 집중하여 개발 
Spock은 BDD 기반 - 비즈니스 요구사항에 집중하여 테스트 케이스 개발 

Spock 의 장점

- Junit - java의 퓨어 자바 코드에 비해 **간결한 Spock - groovy로 작성** 
- Junit은 단위 테스트만 지원한다면, Spock은 **유닛테스트, 통합 테스트, Mocking, Stubbing을 함께 지원**한다.
- **가독성이 좋다.** (given when then 구조), junit은 주석을 이용하여 명시적으로 구분한다.

---

### Question 

- BDD의 full name은 무엇인지 
- java 퓨어코드 vs groovy 문법의 차이 

---

### Basic Grammer 

- def : 동적 타입을 선언하는 예약어 

- setup() 테스트 클래스가 생성될 때에 setup() 안에 메서드 안의 코드가 가장 먼저 실행된다. (유닛 테스트가 실행되기 전에 선행되어야 할 코드를 작성해준다.)


| given  | 테스트가 실행되기 전에 수행되어야할 코드 setup()은 클래스 전역이지만, given은 작성된 테스트 코드 내로 범위가 한정된다. |
| ------ | ------------------------------------------------------------------------- |
| when   | 검증하고 싶은 작업 작성                                                             |
| then   | 검증 값 입력                                                                   |
| expect | 기대하는 수행 동작                                                                |
| where  | 검증하고 싶은 파라미터 값을 추가하여, 조건과 결과만 바꿔가며 테스트 할 수 있다.                            |
|        |                                                                           |

- where 조건이 존재하기 때문에 테스트가 3회 실행된다.

```groovy 
def "테스트 1번"() {  
    given:  
    def testValue = 1  
  
    when:  
    def returnValue = testValue + param  
  
    then:  
    returnValue == result  
  
    where:  
    param | result  
    0     | 1  
    10    | 11  
    100   | 101  
}
```

- 값 검증 
- 실행 횟수 검증 
- 