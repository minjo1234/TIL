

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
public static <T> Predicate <T> distinctByKey(Functino<? super T,?> keyExtractor) {
	Set<Object> seen = ConcurrentHashMap.newKeySet();
	return t -> seen.add(keyExtractor.apply(t))
}
```


#### Predicate -> T타입의 조건을 입력받아 boolean 을 반환하는 함수형 인터페이스.

? super T -> 해당 인자의 상위타입 까지 수용
? extends T -> 해당 인자의 하위 타입까지 가능하도록