

- 자바 8에서 도입된 개념으로 

```
변수에 final을 붙이지 않았지만 
값이 변경되지 않아 final과 유사하게 동작하는 것을 의미합니다
```

- Lambda식에서 자주 접하는 Effectively Final은 

```
for (int i = 1; i <= 12; i++) {  
    int month = i;  
    List<SaleStatusVO> list = vo.stream().filter(d -> d.getSaleDate().getMonthValue() == int).toList();  -> effectively final 에러
}
```

```
for (int i = 1; i <= 12; i++) {  
    int month = i;  
    List<SaleStatusVO> list = vo.stream().filter(d -> d.getSaleDate().getMonthValue() == month).toList();  
}
```


i는 반복문으로 계속 변할 수 있다고 가정되어 **`Effectively`** final의 조건을 충족하지않아 참조가 불가하다.

---

**하지만 람다는 스택에 저장된 값을 읽지 못하는데 

- 지역변수는 스택영역에 저장되며, 블록이 끝나면 제거된다.


-----

**람다식에서 지역변수로 선언된 값을 읽을 수 있는 경우가 존재한다.

- effectively final : 한 번 초기화 된 후 값이 변경되지 않는 변수


여기서는 클로저라는 개