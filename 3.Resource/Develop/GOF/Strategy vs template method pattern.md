
**Blog Name : Template Method vs Strategy Pattern: 언제 어떤 패턴을 사용할까?**

공통점: 데이터를 은닉화 시켜 구현될 수 있도록 도와주는 패턴

알아야할 것 : 특징, 의존의 방향, 제어의 방향

템플릿 메서드 패턴 :
- 의존(dependency)방향  : 자식 -> 부모 (부모가 존재하지 않으면 자식은 존재할 수 없음)
- 제어의 방향 : 부모 -> 자식 (부모가 자식의 구현된 메서드를 호출한다.)
- 특징 : 하위 클래스가 상위 클래스에서 구현되지 못한 부분을 구현 시켜주는 것 






**Background** 

실무에서 자연스럽게 공통 로직을 구현하는 중, 전략 패턴과 템플릿 메서드 패턴을 
언제 어느 상황에 사용해야 하는지 정확히 이해하지 못하고 있다는 생각이 들었다.

둘 다 공통 부모를 가지고 하위 클래스에서 구현체를 구현하지만, 
"공통 로직을 상속받아 재사용하는 것"과 "동적으로 다른 알고리즘을 선택하는 것"의 
차이점이 모호했다.

이번 분석을 통해 두 패턴의 핵심 차이점과 실무에서의 적용 기준을 
명확히 정리하고, 향후 비슷한 상황에서 올바른 패턴을 선택할 수 있는 
가이드라인을 만들고자 한다.

---

 **정적할당 vs 동적할당** 

> 정적할당 : 컴파일 시점에 결정 
> 동적할당 : 런타임에 조건에 따라 다른 구현체를 할당 


정적할당과 동적할당 예시를 들기위해 간단한 코드를 준비해보았습니다.

**정적할당** : Data를 처리하는 추상클래스와 구현체들 

```pi
```

---





---


#### ❌ 단점

1. 클래스 수 증가
- 전략마다 클래스가 필요
- 13개 리소스 = 13개 클래스

1. 클라이언트가 전략을 알아야 함
- 어떤 전략을 사용할지 클라이언트가 결정해야 함



---

### Strategy Pattern 부분

```java
// 1. 인터페이스 정의

public interface AriaResourceHandler {
	AriaResourceType getType();
	CollectedResource convert(AriaResourceResponse.ResourceContent resource);
}

// 2. 각 전략 구현체들이 독립적으로 convert 메서드 구현
public class AriaProjectHandler implements AriaResourceHandler {

@Override
public CollectedResource convert(...) {
// Project 전용 변환 로직
	}
}

public class AriaVPCHandler implements AriaResourceHandler {

@Override
public CollectedResource convert(...) {
// VPC 전용 변환 로직
	}
}

// 3. 런타임에 동적으로 전략 선택
Map<AriaResourceType, AriaResourceHandler> handlerMap = ...;
AriaResourceHandler handler = handlerMap.get(resourceType); // 동적 할당!
```

선택하는 경우 
#### 1. 완전히 다른 처리 방식이 필요한 경우
#### 2. 런타임에 전략 변경이 필요한 경우
#### 3. 각 전략이 독립적으로 진화해야 하는 경우


### Template Method Pattern 부분

```java
// 추상 클래스에서 공통 유틸리티 메서드 제공
public abstract class AbstractAriaResourceHandler implements AriaResourceHandler {

// 공통 로직 (템플릿 메서드들)
protected String extractUuidFromUrl(String resourceUrl) { ... }
protected List<String> extractAdditionalDeploymentUuids(...) { ... }

}

  

// 각 구현체에서 공통 메서드들을 상속받아 사용
public class AriaProjectHandler extends AbstractAriaResourceHandler {
@Override
public CollectedResource convert(...) {

// 공통 메서드들을 상속받아 사용
String uuid = extractUuidFromUrl(resource.getPropertiesStringItem("vpcProfile"));

List<String> additionalIds = extractAdditionalDeploymentUuids(resource);
// ...
	}
}
```


| 구분    | Strategy Pattern | Template Method Pattern |
| ----- | ---------------- | ----------------------- |
| 구조 제약 | ❌ 없음 (완전 자율)     | ✅ 있음 (강제된 구조)           |
| 구현 방식 | 모든 메서드를 독립적으로 구현 | 공통 구조 + 특화 부분만          |
| 유연성   | 높음 (완전 자유)       | 낮음 (구조 제약)              |
| 일관성   | 낮음 (각자 다름)       | 높음 (구조 동일)              |
|       | 예측하기 어려움         | 일관성 보장                  |
|       |                  | 유연성 제한                  |
공통된 부모,  메서드를 가지지만 일관성이 낮은 경우, 동적할당 -> strategy 
공통된 부모, 메서드를 가지지만 일관성이 높은 경우, 정적할당 -> template method 

PortFolio를 하나의 블로그로 올리기. 경로만 주면되니까 좋을듯 ?



그렇다면

하위의 메서드들이 공통적인 메서드가 존재하지만 내부 동작 원리는 많이 다른 경우에는 strategy pattern 

공통적인 메서드의 내부 동작원리까지 비슷하다면 template method pattern 



---

제어흐름 : https://happy-coding-day.tistory.com/93

---






Redis 도입

현재 : ConcurrentHashMap 기반 인메모리 캐시를 이용중 

HashMap은 동시성 제어가 고려되어 있지않게 설계가 되어있지만
ConcurrentHashMap은 이를 고려하여 설계가 되어있다. CAS(Compare-And-Swap) 같은 비동기적인 동시성 제어 기업을 사용한다.

