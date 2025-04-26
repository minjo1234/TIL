
Java에서 DB에 저장된 문자열 값을, Enum 클래스의 값으로 변환하는 방법

1.엔티티 매핑에서 Enum 타입을 사용할 경우 @Enumerated  어노테이션을 사용하는데, 
2.String type으로 enum 타입을 조회하게 될 경우 오류가 발생하여 
(여기서 궁금증 - 어차피 DB에는 varchar로 저장되어있는데 String 으로 보내면 안되는지? - JPA를 통해서 DB를 조회하기 때문에 ) EnumType.valueOf(String string)을 이용한다.

```java
@Enumerated(EnumType.STRING)
private ItemCategory itemCategory; 
```

```java

```


@Convert를 사용하게 될 경우 
- 유지보수성과 관련된 것들이 향상됩니다.
- 


참조 :
https://studyandwrite.tistory.com/496
https://techblog.woowahan.com/2600/