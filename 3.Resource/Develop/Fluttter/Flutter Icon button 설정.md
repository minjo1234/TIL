---
aliases:
  - Flutter Icon button 설정
---

```
appBar: AppBar(  
  leading:  
    IconButton(  
      icon: const Icon(Icons.backspace),  
      onPressed: () {  
  
      },    ),  title: const Text('연모'),  
  actions: [  
    IconButton(  
      icon: const Icon(Icons.search),  
      onPressed: () {  
        // 검색 기능 구현  
      },  
    ),    IconButton(  
      icon: const Icon(Icons.notifications_none),  
      onPressed: () {  
        // 알림 기능 구현  
      },  
    ),  ],  
),
```

---


### 🧭 참고 정리

|속성|위치|타입|설명|
|---|---|---|---|
|`leading`|왼쪽|`Widget?`|기본적으로 '뒤로가기'나 '메뉴' 아이콘에 사용|
|`title`|중앙|`Widget?`|보통 `Text`|
|`actions`|오른쪽|`List<Widget>`|아이콘 버튼이나 메뉴 등 여러 개 가능|

