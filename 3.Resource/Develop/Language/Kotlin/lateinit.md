
kotlin에서 val를 정의하는 경우에 사용한다.

- val는 상수와 같이 변하지 않는 값을 정의할 때 주로 사용한다.
- 클래스의 속성이나 함수의 지역 변수로는 사용 불가능 

그런데 초기의 val를 정의하기가 어려운 경우에 val a = 객체처리가 어려운 경우에  val a = null을 사용해야 한다면 kotlin은 null 사용을 싫어하기 때문에 이를 **지양**하고 있다.


이때 이를 해결할 수 있는게 **"lateinit"** 이라는 변수이다.
변수의 값을 나중에 초기화한다고 선언하는게 lateinit 변수이다.


```kotlin 
fun main() {
	lateinit val text: String 
	val result1 = 30 
	
	text = "Result: $result1""
	println(text);
}
```


#### 사용법

1. 먼저 lateinit 으로 사용하려고 하는 형태만 지정한다.

```kotlin
lateinit var text: String 
```

1.  val로 변수로 값을 지정 
2. 변수 값에 수정이 필요하다면 다시 지정이 가능하다.