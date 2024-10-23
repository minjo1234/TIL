

1.Java Stream 사용

```Java

List<Solution> solutions = solutionRepository.findByProductTypeIdIsNotNull();

// stream 이용
return solutions.stream()
				.
```