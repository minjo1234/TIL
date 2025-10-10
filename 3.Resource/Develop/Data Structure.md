

### Optional 

- Optional.of(T value) -> value null이면 NPE 발생
- Optional.ofNullable(T value) -> value null이면 Optional.empty() 반환된다.
  -> 이 상태에서 Optional.get()을 사용하면 `NoSuchElementException` 이 발생한다.


Optional.empty() 란 // 값 자체없음

### Set 

LinkedHashSet - 순서유지, HashSet보다 성능은 느림, 중복은 허용하지않음
HashSet - 순서를 보장하지 않음**, 접근 속도 빠르다.