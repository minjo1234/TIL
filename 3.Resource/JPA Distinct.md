

###  1.Java Stream 사용 - 모든 필드가 동일

```Java

List<Solution> solutions = solutionRepository.findByProductTypeIdIsNotNull();

// stream 이용
return solutions.stream()
				.distinct
				.limit(1)
				.collect(Collecters.toLsit());
				
```

### 2.특정 컬럼을 기준으로 중복제거


```java

```