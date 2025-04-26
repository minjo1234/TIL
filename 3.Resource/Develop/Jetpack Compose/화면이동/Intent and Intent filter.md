
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

---

### Intent vs Navigation 

Intent : 새로운 `Activity`를 시작하거나 다른 앱의 특정 기능을 호출할 때 사용

```
Intent intent = new Intent(CurrentActivity.this, NextActivity.class); intent.putExtra("key", "value"); // 데이터 전달 startActivity(intent);
```

----

Navigation : 단일 Activity 내에서 여러 fragment 간의 이동을 관리하거나, 복잡한 화면 흐름을 쉽게 처리할 수 있다.

---


|**항목**|**Intent**|**Navigation**|
|---|---|---|
|**주 사용 대상**|Activity 간 이동|Fragment 간 이동|
|**데이터 전달**|`putExtra()`로 key-value 전달|Safe Args를 통한 타입 안전한 데이터 전달|
|**백스택 관리**|수동으로 처리 (`finish()` 등 호출 필요)|자동으로 백스택 관리|
|**사용 편의성**|단순한 경우에 적합|복잡한 네비게이션 흐름에 적합|
|**기능 확장성**|다른 앱 호출 가능 (암시적 Intent 사용)|앱 내부의 화면 이동에 특화|

---
