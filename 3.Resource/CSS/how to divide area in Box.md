
1.h-1/3, h-2/3 

2.flex-[number]

----

만약 영역을 지정했는데 넘친다면 ?
- 스크롤을 사용한다, overflow-y 설정

클러드 구현에 대한 추천도 받는다.

![[Pasted image 20251228160951.png]]

LocalStorage로 구현하도록 했다. (보안이 필요한 것은 아니므로)

- 변화가 가능한것은 Switch 라는 명으로 구현한다 -> LanguageSwitch 

---

### 알게된 점 

1.fs 모듈은 Node.js 서버 전용 : 브라우저에서 실행 불가 (서버 컴포넌트에서만 실행가능)
2.'use client' 컴포넌트는 브라우저에서 실행되므로 fs를 사용할 수 없다.

  LanguageContext 저장 시스템
  1. localStorage: 브라우저에 영구 저장 (클라이언트 전용)
  2. Cookie: 서버+클라이언트 모두 접근 가능 (HTTP 요청 시  자동 전송)
  3. 이중 저장 이유: 서버 컴포넌트는 localStorage에 접근 불가 → 쿠키 필요
