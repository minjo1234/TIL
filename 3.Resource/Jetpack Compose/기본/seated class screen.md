### 1.경로 관리

```kotlin
sealed class Screen(val route: String) {
	object Splash = Screen(route = "splash_screen")
	object Home : Screen(route = "home")
	
}
```


### 2.쉽게 모바일에서 화면을 추가할 수 있습니다.
