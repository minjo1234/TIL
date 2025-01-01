
### 1.화면 간 이동 (Navigation)

NavController는 Jetpack Compose에서 네비게이션에서 화면 전환과 상태 관리를 담당하는 핵심 객체

#### 1.화면 간 이동 (navigation)

- 특정 화면으로 이동하거나 뒤로 가기수행
- navigate(route: String) 메서드를 사용하여 지정된 경로를 이동

```kotlin
navController.navigates(Screen.Home.route)
```


- 특정 화면만 남기고 이동할 수 있습니다.
  
```kotlin
navController.navigate("home_screen") { popUpTo("login_screen") { inclusive = true } // login_screen 제거 }`
```

- 현재 경로 추척

```kotlin
val currentRoute = navController.currentBackStackEntry?.destination?.route

```


---

### Navigate()  vs popBackStack()


navController.popBackStack() : 현재 화면을 스택에서 제거하고 됟
