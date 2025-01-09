
`Activity` 는 앱의 단일 화면을 종료합니다.

---

1.Intent 는 시작할 활동을 설명하고 필요한 정보를 전달할 수 있다.
2.Intent 라고 하는 것을 startActivity()에 전달하여 Activity의 새 인스턴스를 시작할 수 있습니다.
3.해당 결과를 return 받고싶은 경우 onActivityResult()를 사용하여 결과를 return 받을 수 있다.

---

암시적 Intent : 

startActivity를 이용하여 Intent 객체로 화면 이동을 할 수 있다.

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

명시적 Intent : 


```kotlin
val sendIntent = Intent().apply {
	action = Intent.ACTION.SEND
	putExtra(Intent.EXTRA_TEXT, textMessage)
} 

// verify that the intent will resolve to an activity
if (sendIntent.resolveActivity9packageManager) != null) {
	startActivity(sendIntent)
}
```