
**Blog Name : 실무에서 보는 디자인 패턴: Template Method vs Strategy Pattern**


#### ❌ 단점

1. 클래스 수 증가
- 전략마다 클래스가 필요
- 13개 리소스 = 13개 클래스

1. 클라이언트가 전략을 알아야 함
- 어떤 전략을 사용할지 클라이언트가 결정해야 함


| 구분    | Strategy Pattern | Template Method Pattern |
| ----- | ---------------- | ----------------------- |
| 구조 제약 | ❌ 없음 (완전 자율)     | ✅ 있음 (강제된 구조)           |
| 구현 방식 | 모든 메서드를 독립적으로 구현 | 공통 구조 + 특화 부분만          |
| 유연성   | 높음 (완전 자유)       | 낮음 (구조 제약)              |
| 일관성   | 낮음 (각자 다름)       | 높음 (구조 동일)              |
|       | 예측하기 어려움         | 일관성 보장                  |
|       |                  | 유연성 제한                  |


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


---
