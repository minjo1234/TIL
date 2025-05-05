---
aliases:
  - Flutter 문법
tags:
  - flutter
author: Min Jo
created: 2025-05-05
---
# Flutter 문법 
---


### Scaffold - 기본적인 뼈대를 잡아주는 요소 

| 속성                     | 설명                    |
| ---------------------- | --------------------- |
| `appBar`               | 상단 바 (타이틀, 뒤로가기 버튼 등) |
| `body`                 | 본문 내용 (화면의 메인 부분)     |
| `bottomNavigationBar`  | 하단 탭바 (화면 전환을 위한 버튼들) |
| `floatingActionButton` | 화면 우하단의 동그란 버튼        |
| `drawer`               | 좌측에서 나오는 슬라이드 메뉴      |
| `backgroundColor`      | 배경 색상 설정              |

---


firbase는 서버역할을 해준다.

## 📱 예시: Flutter로 SNS 앱 만들기

- **Flutter**로 UI 디자인하고,
- **Firebase Auth**로 로그인 기능 만들고,
- **Firestore**로 게시글 저장하고 불러오고,
- **Storage**로 이미지 업로드,
- **Messaging**으로 알림 보내기

→ 이렇게 **서버 개발 없이도** 기능이 다 들어간 앱을 만들 수 있어요!


---

### Column (children)
  ㄴ Container (child)
	  ㄴ Center (child)
			ㄴ Text



### 의문 1 

그냥 Text 적으면 되는데 child까지 적는 이유가 뭘까 ?

### 2. ✅ 이렇게는 됩니다:

dart

CopyEdit

`Container(   child: Text('안녕') )`

여기서 `child:`는 **Container라는 위젯이 갖고 있는 '속성(property)' 중 하나**예요.  
그래서 Flutter는 "아~ 이 Text는 Container 안에 들어가는 자식이구나" 하고 이해합니다.


child는 이 위젯이 누구의 자식이 누구인지 `Flutter에게 알려주는 약속된 문법`


---

