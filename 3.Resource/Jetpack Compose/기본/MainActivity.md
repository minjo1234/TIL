
```kotlin
class MainActivity : ComponentActivity() {  
    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        enableEdgeToEdge()  
        setContent {  
            GreetingCardTheme {  
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->  
                    Greeting(  
                        name = "Android",  
                        modifier = Modifier.padding(innerPadding)  
                    )  
                }  
            }        }    }  
}

```

- onCreate : 실행시에 반드시 실행되는 파일
- enableEdgeToEdge() : 앱 콘텐츠의 화면 가장 자리까지 확장해서 상태바 뒤에도 사용
  (게임개발에서 주로 사용하다가 트랜디한 모바일 디자인에도 적용하는 경우에 사용)
- setContent : UI구성
- theme : 글꼴 , 색상 , 테마 정의
- Scaffold : 앱의 기본적인 구조의 최상위 구조
- modifier : 수정자  
- 