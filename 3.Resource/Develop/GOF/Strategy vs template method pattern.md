

Strategy Pattern : 런타임에 알고리즘 변경이 가능하다.

- 확장성 좋음: 새로운 리소스 타입 추가시 인터페이스만 구현 
- 기존 코드 수정 없이 확장 가능 

코드 중복 제거
- 공통 로직은 인터페이스에 정의
- 각 전략별 특화 로직만 구현

#### ❌ 단점

1. 클래스 수 증가
- 전략마다 클래스가 필요
- 13개 리소스 = 13개 클래스

1. 클라이언트가 전략을 알아야 함
- 어떤 전략을 사용할지 클라이언트가 결정해야 함

```java
package com.clovirone.vmware.aria.resource;

import com.clovircm.domain.aria.resource.AriaResourceType;
import com.clovircm.domain.aria.resource.additionalInfo.AriaResourceAdditionalInfo;
import com.clovircm.domain.aria.resource.billingInfo.AriaBillingInfo;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;
import com.fasterxml.jackson.annotation.JsonSubTypes;
import com.fasterxml.jackson.annotation.JsonTypeInfo;

import java.time.LocalDateTime;
import java.util.List;

  

@JsonIgnoreProperties(ignoreUnknown = true)
@JsonTypeInfo(use = JsonTypeInfo.Id.NAME, property = "type")
@JsonSubTypes({

@JsonSubTypes.Type(value = CollectedResourceAIP.class, name = "CollectedResourceAIP"),

@JsonSubTypes.Type(value = CollectedResourcePeering.class, name = "CollectedResourcePeering"),

@JsonSubTypes.Type(value = CollectedResourceProject.class, name = "CollectedResourceProject"),

@JsonSubTypes.Type(value = CollectedResourceSegment.class, name = "CollectedResourceSegment"),

@JsonSubTypes.Type(value = CollectedResourceVM.class, name = "CollectedResourceVM"),

@JsonSubTypes.Type(value = CollectedResourceBlockDisk.class, name = "CollectedResourceBlockDisk"),

@JsonSubTypes.Type(value = CollectedResourceNfs.class, name = "CollectedResourceNfs"),

@JsonSubTypes.Type(value = CollectedResourceVPC.class, name = "CollectedResourceVPC"),

@JsonSubTypes.Type(value = CollectedResourceVpcFireWall.class, name = "CollectedResourceVpcFireWall"),

@JsonSubTypes.Type(value = CollectedResourceCluster.class, name = "CollectedResourceCluster"),

@JsonSubTypes.Type(value = CollectedResourceNLB.class, name="CollectedResourceNLB"),

@JsonSubTypes.Type(value = CollectedResourceSecurityGroup.class, name = "CollectedResourceSecurityGroup"),

@JsonSubTypes.Type(value = CollectedResourceVMFW.class, name = "CollectedResourceVMFW")

})

public interface CollectedResource {

String getResourceUuId();

String getResourceName();

LocalDateTime getCreatedAt();

AriaResourceType getResourceType();

AriaResourceAdditionalInfo getAdditionalInfo();

List<String> getAdditionalDeploymentUuids();

AriaBillingInfo getBillingInfo();

  
  

}
```


단순한 메서드 선언은 template method가 아니다. 


```java
// 전략 인터페이스
public interface CollectedResource { ... }

// 구체적인 전략들
public class CollectedResourceVM implements CollectedResource {
// VM 전략: VM에 특화된 방식으로 모든 메서드 구현
}

public class CollectedResourceSegment implements CollectedResource {
// Segment 전략: Segment에 특화된 방식으로 모든 메서드 구현
}
```


이런식으로 공통구조 + 특화로직존재하면 template method 

```java
@JsonIgnore

@Override

public String getSearchField() {

Map<String,Object> searchFields = new HashMap<>();

searchFields.put("cidr", networkCidr);

return RegexUtil.getKeyValueToString(searchFields);

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

구조제약이 있냐 없냐의 차이 




완전히 다른 방식이 필요한 경우 
런타임에 전략 변경이 필요한지
각 전략이 독립적으로 진화 

공통 구조
일관성 
공통 로직

|구분|Strategy Pattern|Template Method Pattern|
|---|---|---|
|변경 의미|"어떤 알고리즘을 사용할까?"|"어떤 구현체를 사용할까?"|
|변경 결과|완전히 다른 처리 방식|같은 구조, 다른 내용|
|예시|VM 처리 vs Segment 처리|VM 검색 vs Segment 검색|



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
