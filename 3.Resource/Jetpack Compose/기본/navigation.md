
### 1.화면 간 이동 (Navigation)

NavController는 Jetpack Compose에서 네비게이션에서 화면 전환과 상태 관리를 담당하는 핵심 객체

#### 1.화면 간 이동 (navigation)

- 특정 화면으로 이동하거나 뒤로 가기수행
- navigate(route: String) 메서드를 사용하여 지정된 경로를 이동

`navController.navigates(Screen.Home.route)`
`navController.navigate("home_screen") { popUpTo("login_screen") { inclusive = true } // login_screen 제거 }`

### 2.네비게이션 상태 관리


### 3.인자 전달
