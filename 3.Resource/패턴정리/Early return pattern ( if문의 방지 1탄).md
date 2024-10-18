
참조 : https://woonys.tistory.com/209

---
### Code Readability "Prefer early return style"


```java
 
> public String returnStuff(SomeObject argument1, SomeObject argument2) {
    if (argument1.isValid()) {
        if (argument2.isValid()) {
            SomeObject otherVal1 = doSomeStuff(argument1, argument2)

            if (otherVal1.isValid()) {
                SomeObject otherVal2 = doAnotherStuff(otherVal1)

                if (otherVal2.isValid()) {
                    return "Stuff";
                } else {
                    throw new Exception();
                }
            } else {
                throw new Exception();
            }
        } else {
            throw new Exception();
        }
    } else {
        throw new Exception();
    }
}

```


<u>
코드의 비선형적인 흐름이라 - nest(계속 if문만 따라가서 파고파고 하는 형식)
</u>


이는 또한 몇 가지 안티 패턴을 포함한다.

- [Else is considered smelly](https://wiki.c2.com/?ElseConsideredSmelly): 조건이 복잡할 경우 `else`문은 두 배로 복잡해진다. 왜냐면 읽는 사람은 그 복잡한 조건을 또 뒤집어야 하기 때문이다. 심지어 만약 `if` 블록이 크다면, 무슨 조건을 정했는지 까먹기 쉽다. 따라서 중첩된 `if`와 `else`는 독자로 하여금 혼란스럽게 한다.
- [Arrow anti-pattern](https://wiki.c2.com/?ArrowAntiPattern)은 코드의 모양이 마치 화살과 같다고 해서 붙여진 이름인데, 이는 중첩된 조건 및 루프로 인해서 만들어진다.

---
## **Return Early**

``` java
public String returnStuff(SomeObject argument1, SomeObject argument2){
      if (!argument1.isValid()) {
            throw new Exception();
      }

      if (!argument2.isValid()) {
            throw new Exception();
      }

      SomeObject otherVal1 = doSomeStuff(argument1, argument2);

      if (!otherVal1.isValid()) {
            throw new Exception();
      }

      SomeObject otherVal2 = doAnotherStuff(otherVal1);

      if (!otherVal2.isValid()) {
            throw new Exception();
      }

      return "Stuff";
}
```


- 인덴테이션이 오직 한 뎁스만 들어가있다. 이렇게 되면 선형적으로(위에서 아래로 linear) 읽을 수 있다.
- 예상 결과를 함수 끝에서 빠르게 찾을 수 있다. (if문은 전부 예외 관련 케이스이니 예상 결과를 바로 보고 싶으면 그냥 맨 밑만 확인하면 끝)
- 이 사고 과정을 활용하면 에러를 가장 먼저 찾는데 주의를 기울이고 비즈니스 로직을 안정적으로 구현하는 걸 나중에 할 수 있다. 이렇게 할 경우, 불필요한 버그를 피할 수 있다.
- 예외 케이스를 먼저 처리하는 `fail-first` 마인드셋은 TDD(바로 그 TDD!)와 유사하다. 이는 코드를 테스트하기 훨씬 쉽게 해준다.
- 함수는 에러가 발생하는 즉시 종료되기에, 의도하지 않게 코드가 실행될 가능성을 방지하게 한다.


---

### 근데 이러한 게 더욱 안 좋게 작용하는 경우도 존재하는데

- [함수는 오직 하나의 exit point를 가져야만 한다.](링크없음)  - 단일 엔트리, 단일 종료(Single Entry, Single Exit, SESE)개념은 C, 어셈블리어와 같이 명시적인 자원 관리를 가진 언어에서 비롯된다. 자원을 수동으로 관리하지 않는 경우에는 오래된 규칙을 고수할 필요가 없는데 SESE 코드는 현대와 맞지않는 공룡 코드와 같고 , 즉 코드의 이해를 오히려 방해할 수 있다.
- [자원(Resource) cleaning → 이게 비판점인가?(Q)]()  - Try, catch, and finally 문을 사용하면
  try 블록에서 어떤 가능한 예외든 포착한 다음 마지막 final 블록에서 리소스를 해제해 메모리 누수가 없도록 한다. 
  using 문은 블록 안에서 자원 사용을 허용하며, 비록 종료가 조기에 일어날 지라도 자원이 사용된 후 자동으로  폐기되게 한다.
  이러한 컨셉은 함수 실행을 종료할 때 사용된 리소스를 처리하는 동시에 return early 규칙을 사용할 수 있게 한다.

- <font color="#b2a2c7">로깅(Loggin)과 디버깅(Debugging)</font> - 로깅을 예외처리를 한 이후에 마지막에 다는 것이 규칙이기 때문에 오히려 개발자 관점에서 불편할 수 있는데 , 개발자가 예외처리 구역마다 테스트해볼 logging을 작성하는 것도 하나의 방법이다.
  
- <font color="#b2a2c7">종료 지점이 많으면 가독성에 영향을 끼친다</font>. - (Multiple exit points affect readability) - 한줄에 너무 많은 코드를 작성하게 되면 읽기도 힘든데 이걸 제한하기 위해 Bouncer 패턴과 extract method 패턴이 반드시 사용되어야 한다

---

> ###  **Code style is subjective** : 적절한 경우에만 사용해라  ### 


``` java
private void validateArgument1(SomeObject argument1) {
        if(!argument1.isValid()) {
                throw new Exception();
        }
        if(!argument2.isValid()) {
                throw new Exception();
        }
}

public void doStuff(String argument1) {
        validateArgument(argument1);
        // do more stuff;
}

``` 


KISS YAGNI(Keep it Simple, Stupid You Arent Gonna Need it) 

- 첫번째 접근과 두 번째 접근을 비교할 때, 첫번째 접근에서의 코드 줄이 더 길 뿐더러 복잡도도 높다. 하지만, “return early” 사고 방식으로 쓰여졌기에 향후 기능 개선에 더욱 열려있는 구조임. 하지만 이러한 사고 방식은 KISS와 YAGNI 규칙을 위반하게 되는데, 각각 “Keep It Simple, Stupid(단순하게 해, 멍청아)”와 “**Y**ou **A**ren’t **G**onna **N**eed **I**t(그건 필요하지 않게 될 걸)”이다. 그러니 만약 나중에 “return early” 패턴이 필요할 경우 이 방식으로 변경하는 게 쉽다.
- 두 번째 접근은 훨씬 간결하고 읽기도 좋다. 코드가 정확히 요점을 짚었기에 나라면 이 문제에서 두 번째 접근 방식을 선택할 것이다.

---

## **Conclusion**

> [!NOTE] 결론의글 
> >
> return early 패턴은 함수가 복잡해지는 것을 방지하는 훌륭한 방법이다. 하지만 이것이 모든 상황에 다 적용할 수 있다는 뜻은 아니다. 때때로(특히 복잡한 비즈니스 로직에서는) 필연적으로 중첩된 if문을 만들어야 할 수밖에 없는데, 특히 코드를 다른 함수로 추출하는 옵션에서는 그렇다.
> 
> 더 나은 접근 방법은 각 팀에서 그들끼리 정보를 공유하고 각 케이스에 대해 어떤 패턴을 사용하는 게 좋을지 결정하며 모두가 프로그래밍할 때 비슷한 마인드셋을 갖고 있다고 확신하는 등 align을 맞추는 것이다. 개발자들은 코드를 쓰는 데보다 읽는 데 더 많은 시간을 들이기 때문에 팀원들 간의 align이 모두에게 긍정적인 경험을 제공할 것이다. = 팀원들끼리 뭐 쓸지 조율하는게 좋을 듯 
> 



-- bouncer pattern , extract pattern 공부해야함.
-- 프록시패턴 
-- service serviceImpl ISP
-- 전략패턴
-- factory method 패턴
-- generic

