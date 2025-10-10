

### Optional 

- Optional.of(T value) -> value null이면 NPE 발생
- Optional.ofNullable(T value) -> value null이면 Optional.empty() 반환된다.
  -> 이 상태에서 Optional.get()을 사용하면 `NoSuchElementException` 이 발생한다.


Optional.empty() 란 // 값 자체없음



string.isEmpty 빈 문자열인경우, null 인경우 true - npe 발생

```
// 문제: NPE 발생 가능

vm.getPrimaryIp().isEmpty()


// 해결: null 체크 후 isEmpty() 호출

vm.getPrimaryIp() == null || vm.getPrimaryIp().isEmpty()
```

null 체크와 , ""문자열 확인한번에 

ObjectsUtils.isEmpty


---

### Set 

LinkedHashSet - 순서유지, HashSet보다 성능은 느림, 중복은 허용하지않음
HashSet - 순서를 보장하지 않음**, 접근 속도 빠르다.

---

### SingleTonList 

- 크기작음 Immuable  - https://prohannah.tistory.com/85