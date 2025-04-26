#### UI 안에서 동작하는 크기, 위치, 패딩 이벤트 등을 정의한다.


`개발팁
모든 composable이 modifier를 허용하고  ui 를 내보내는  첫 번째 하위요소에 modifier를 정의한다. 


### Example

```kotlin
@Composable
fun Size(modifier: Modifier = Modifier) {
	Surface (
		color = Color.red
		modifier = modifier.fillMaxSize()
	) {
	}
}
```