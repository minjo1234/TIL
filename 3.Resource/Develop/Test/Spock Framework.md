
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


### 코드 작성 예시

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

---

- 값 검증 
- 실행 횟수 검증 은 어떤식으로 진행될까 ?



### Object  (Mock vs Stub)

- mock (stubbing vs mocking) - 메서드에서 수신하는 호출을 등록해서 실제 호출이 잘 되었는지(호출여부, 호출 횟수, 호출 인자) , (메서드 호출 여부/횟수 검증, 행위(behavior) 이 메서드가 실제로 호출되었는가? 몇? 번? 어떤 인자로?, 필요시 정의가능, 주 목적은 아님, 호출 여부, 횟수, 순서를 반드시 검증)


- stub (stubbing ) - 호출 결과를 고정된 값으로 미리 정의, 실제 호출 여부나 횟수를 신경 쓰지 않는다. (고정된 리턴값 제공, 상태(state) 메서드를 어떤 값을 반환해야 하는가 ?, 미리 정의해둔 값을 반환, 호출 여부 따지지않음 )


stub은 몇 번 호출되었는지 물어볼 수 없는 차이가 존재한다.


**내가 궁금했던 점** 

- 어떤 상황에 Mock을 쓰고 어떤 상황에 Stub을 사용해야 할까 ?





---


### Question 

- BDD의 full name은 무엇인지 
- java 퓨어코드 vs groovy 문법의 차이 
- stubbing vs mocking 



대

Mock vs Stub (Inflearn) : https://www.inflearn.com/community/questions/1257985/mock과-stub의-차이가-아직-잘-구분되지-않습니다?srsltid=AfmBOorP4zYvDdbFegNlNvvkM3Noypue7QIC5zpycdo8SOxtpKG0CEvc

www.chatgpt.com

mock과 stub의 차이를 테스크코드에서 확인하고 싶으니까 간단한 테스트 코드좀 만들어줘 mock 과 stub의 차이점을 확인할수있도록 - spock framework 



근데 mock은 실제로 객체의 값도 확인가능하고 몇번 선언되었는지도 확인가능한데 
stub은 이미 값을 ㅅ