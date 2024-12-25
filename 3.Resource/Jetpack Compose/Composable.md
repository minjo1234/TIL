
1.jetpack compose는 @Composable이 콤포즈 UI 뷰를 반환한다.
2.층(@Composable) 안에 층(@Composable) -> 층(@Composable이) 존재하는 구조이다.

3.@Preview 미리보기 기능을 수행한다.

Surface -> 레이아웃 구성
// Column, Row, Box 

modifier.padding(24.dp)


```
Box( modifier = Modifier .sizeIn(maxWidth = 300.dp, maxHeight = 400.dp) .verticalScroll(rememberScrollState()) // 세로 스크롤 추가 .background(Color.Cyan) ) { Column { for (i in 1..50) { Text("항목 $i", modifier = Modifier.padding(8.dp)) } }

```

