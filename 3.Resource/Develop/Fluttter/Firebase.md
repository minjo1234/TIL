---
aliases:
  - Firebase
tags:
  - Firebase
  - app
author: Min Jo
created: 2025-05-05
---


# Firebase 
---

나는 백엔드 개발자이다. 하지만 동시에 풀스택을 하는 개발자이기도하다(Spring Boot, Vue.js)

혼자 간단한 것을 개발하더라도 엔티티를 설계하고, 비즈니스로직을 생각하는데 시간을 많이 들이다보니 생산성을 높이는 방법을 고민해왔다.  
이제부터 Firebase를 이용하여 간단한 앱의 백엔드 개발을 대체해보려고한다.

앞으로 단계별로 FireBase의 기능들을 공유하고자한다.

> 개발언어 : Flutter 
> 백엔드 : Firebase 

---

그래서 Firebase를 간략히 설명하는 시간을 가지려고하는데, 

### 🔥 Firebase는 뭐냐면...

> 서버 없이도 앱을 만들 수 있게 도와주는 백엔드 서비스 묶음 

내가 서버를 직접 만들 필요 없이, Firebase가 서버처럼 작동하는
대부분의 앱에서 필요한 **백엔드 역할을 해주는 서비스 플랫폼**이다.

---

## 📦 Firebase가 제공하는 백엔드 기능들

|기능|설명|
|---|---|
|**Authentication**|로그인/회원가입/소셜 로그인 등|
|**Cloud Firestore**|실시간 NoSQL 데이터베이스|
|**Realtime Database**|실시간 데이터 동기화 (IoT 등)|
|**Cloud Storage**|이미지/파일 업로드 & 다운로드|
|**Cloud Functions**|서버에서 로직 처리 (Node.js 기반)|
|**Cloud Messaging**|푸시 알림 전송|
|**Analytics**|사용자 분석, 이벤트 추적|
|**Crashlytics**|앱 오류 추적 및 리포트|

---

### ❓ 그럼 완전히 백엔드 대체 가능할까 

- ❗ **복잡한 비즈니스 로직**, **보안 처리**, **맞춤형 서버**가 필요할 땐 → Cloud Functions 사용하거나 별도 서버 구축 필요하다.
✔️ **중소형 앱**에는 완전히 대체 가능하다.

---
### 🔍 한 줄 요약:

> **Firebase는 서버 없이도 앱을 만들 수 있게 도와주는 "백엔드 서비스"다.**

---
