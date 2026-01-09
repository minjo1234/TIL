
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


⏺ ★ Insight ─────────────────────────────────────
  Context + localStorage 설계 핵심 5단계
  1. createContext: 전역 상태 저장소 생성
  2. Provider: 상태와 함수를 제공하는 컴포넌트
  3. Custom Hook: useContext를 감싸는 편리한 훅
  4. Root Layout: 앱 최상위에 Provider 배치
  5. 사용: 모든 컴포넌트에서 Hook으로 접근
  ────────────────────────────────────────
  📋 전체 설계 로드맵

  6. TypeScript 타입 정의
     ↓
  7. createContext 생성
     ↓
  8. Provider 컴포넌트 작성
     ↓
  9. Custom Hook 작성
     ↓
  10. Root Layout에 Provider 추가
     ↓
  11. 컴포넌트에서 사용
     ↓
  12. (선택) 서버 컴포넌트 지원

  ---
  🎯 예제: ThemeContext (다크모드) 만들기

  localStorage로 테마를 저장하는 시스템을 처음부터 만들어보겠습니다.

  ---
  ✅ 1단계: TypeScript 타입 정의

  목적: Context에서 다룰 데이터 구조와 함수 시그니처 정의

  // src/contexts/ThemeContext.tsx
  'use client';

  import { createContext, useContext, useState, useEffect, ReactNode, useMemo, useCallback } from 'react';

  // ① 타입 정의: 가능한 테마 값
  type Theme = 'light' | 'dark' | 'auto';

  // ② 인터페이스 정의: Context가 제공할 값들
  interface ThemeContextType {
    theme: Theme;                    // 현재 테마
    setTheme: (theme: Theme) => void; // 테마 설정 함수
    toggleTheme: () => void;         // 테마 토글 함수
  }


1.타입 정의 

```bash
type Language = 'ko' | 'en';
```

2.인터페이스 정의

```bash
interface LanagueaContextType { 
	language: Language; 
	setLanguage: (lang: Language) => void;
	toggleLanguage: () => void;
}
```

3.createContext

```
const LanguageContext = createContext<LanguageContextType | undefined>(undefined);
```

4.Provider 

```

```

---

`useMemo`는 리액트 컴포넌트가 렌더링될 때, 결과 값을 메모리(캐시)에 저장해두었다가 의존성 배열이 바뀔 때만 다시 계산, 의존성 배열이란 ?

첫 번째 인자 : 실행할 함수 
두 번째 인자 : 의존성 배열 

```typescript 
const value = useMemo(  
() => ({ language, setLanguage, toggleLanguage }),  
  [language, setLanguage, toggleLanguage]  
);
```

// language, setLanguage, toggleLanguage 중 하나의 값이 변하면 함수가 작동한다.

---

### Context API가 데이터를 어떻게 포장해서 전달하는지 

`createContext`를 호출하는 순간, 리액트는 두 가지 특별한 컴포넌트를 생성합니다.
- **`LanguageContext.Provider`**: 데이터를 주는 놈
- **`LanguageContext.Consumer`**: 데이터를 받는 놈 (요즘은 `useContext`로 대체)

---

### Provider 
- 자식 컴포넌트에서 
- `useMemo`를 사용하면 자식 컴포넌트에서 사용한 값에 대한 변경에 대한 탐지를 자동으로 한다.
- LanguageContext.Provider value=value 형식으로 자식에게 값을 전달한다.
- useMemo는 캐싱을 담당한다 (값이 변경되었는지를 계속 참조)

1.개발 시점 순서
- createContext() - 컨텍스트 생성
- Provider 컴포넌트  - 데이터 제공자 
- useContext() - 데이터 사용자

2.실행 시점 순서 (앱 실행)
- createContext() - 메모리에 방송 채널 생성
- ② Provider 렌더링 - value를 채널에 방송 시작
- ③ useContext() 호출 - 채널에서 value 수신

1. 핵심 포인트:
	- createContext는 한 번만 실행 (모듈 로드 시)
	- Provider는 렌더링될 때마다 실행
	- useContext는 호출할 때마다 최신 value 반환

  2. 핵심: React의 상태 변경 → 자동 리렌더링
    - setLanguageState 호출 → React가 감지
    - Provider 리렌더링 → 새 value 생성
    - useContext 사용하는 컴포넌트들 자동 리렌더링

  3. React 내부에서 상태 변경 감지
  4. LanguageProvider 전체가 다시 렌더링됨
  5. Provider의 value가 새로 계산됨
  6. useContext를 사용하는 모든 컴포넌트가 자동 리렌더링

---

  useMemo 없으면:
  const value = { language, setLanguage, toggleLanguage };
  // 매 렌더링마다 새 객체 생성
  // → 객체 참조가 계속 바뀜
  // → Provider value가 바뀐 것으로 인식
  // → useContext 사용하는 모든 컴포넌트 매번 리렌더링 (낭 비!)

  useMemo 있으면:
  const value = useMemo(
    () => ({ language, setLanguage, toggleLanguage }),
    [language, setLanguage, toggleLanguage]
  );
  // language가 실제로 바뀔 때만 새 객체 생성
  // → 안 바뀌면 이전 객체 재사용 (같은 참조)
  // → Provider value가 안 바뀐 것으로 인식
  // → 불필요한 리렌더링 방지 (최적화!)
 // LanguageProvider 자체가 재렌더링될 때 useMemo가 없으면 다른 페이지가 로드될때 값의 변화가 없더라도, 매번 새 객체가 만들어진다.

  언제 Provider가 재렌더링될까?
  1. language 변경될 때 ← 이건 당연히 새 value 필요
  2. 부모 컴포넌트가 재렌더링될 때 ← 문제!
  3. Provider 내부에 다른 상태 추가되면 ← 문제!

  실제 예시

  // layout.tsx
  <ThemeProvider>  {/* ← 테마 변경 시 재렌더링 */}
    <LanguageProvider>  {/* ← 덩달아 재렌더링! */}
      <Header />
      <Footer />
    </LanguageProvider>
  </ThemeProvider>
```typescript
  // layout.tsx
  <ThemeProvider>
    <LanguageProvider>  {/* ← 이게 재렌더링될 때 */}
      <Header />
      <main>{children}</main>  {/* ← 페이지 전환 (children 바뀜) */}
      <Footer />
    </LanguageProvider>
  </ThemeProvider>

```


  페이지 전환 시:
  
  / → /about 페이지 이동
    ↓
  children만 바뀜 (HomePage → AboutPage)
    ↓
  LanguageProvider는 재렌더링 안 됨 ✅
    ↓
  useMemo 실행 안 됨

  LanguageProvider가 재렌더링되는 경우:
  1. language 변경 (버튼 클릭)
  2. 부모(ThemeProvider)가 재렌더링 (테마 변경)
  3. Provider 내부에 다른 상태 추가했을 때

---

⏺ 완벽합니다! 정확히 이해하셨어요! 👏

  // 부모(ThemeProvider) 재렌더링
  ThemeProvider 재렌더링
    ↓
  LanguageProvider도 재렌더링 (children이니까)
    ↓
  useMemo 없으면: value = { ... } 새 객체 생성
    ↓
  React: "객체 참조가 바뀌었네!" → 모든 useContext 사용처  리렌더링 ❌

  // useMemo 있으면:
  LanguageProvider 재렌더링
    ↓
  useMemo: "language 안 바뀌었네? 이전 객체 재사용!"
    ↓
  React: "value 참조가 같네!" → 리렌더링 안 함 ✅

  핵심:
  - Provider 컴포넌트는 재렌더링됨
  - 하지만 value 객체는 안 만들어짐 (캐시된 거 재사용)
  - 참조가 같으니 children들은 리렌더링 안 됨

  SKILL.md에 이 부분 추가해드릴까요?
  ⎿ Stop says: Hookify import error: No module named 
    'hookify'

---

mdx파일들은 서버에서만 실행, cookie, localstorage는 클라이언트에서 제공 

  서버에서 쿠키 읽기:
  - getCookie()는 클라이언트용 (document.cookie)
  - cookies()는 서버용 (Next.js 제공)

언제 cookies를 사용하고 언제 getCookie()를 사용해야할까 ??

컴포넌트에서는 await 사용이 불가능하다.

  1. 서버 컴포넌트 (async 가능) → cookies()
  2. 클라이언트 컴포넌트 ('use client') → getCookie()

QDVO 

25년 4월 연금계좌에서 과세이연 없앤다고 발표했음

국가 보조금 
지자체 보조금

---

  ✅ Mock으로 만드는 경우

  CommandEvent event = Mock()  // interface → 인스턴스 생성 불가

  - 인터페이스나 추상 클래스: 직접 생성 불가능
  - 복잡한 의존성: 생성하기 어려운 객체
  - 행동(behavior) 검증: 메서드 호출을 확인해야 할 때

  ✅ 실제 객체로 만드는 경우

  AriaDeployRequest request = AriaDeployRequest.builder()
      .id(1L)
      .requestAction(RequestAction.CREATE)
      .build()


---

|                                                        |               |              |              |
| ------------------------------------------------------ | ------------- | ------------ | ------------ |
| Microsoft Certified: Azure for SAP Workloads Specialty | CF47U6-9629EF | Dec 27, 2025 | Dec 28, 2026 |

후처리 작업실패시 완료 
실패시 완료 

---


nextjs와 spring boot를 같이 사용하려는 경우 프록시와 CQRS 설정을 해야한다고 한다.

nextjs, Spring CQRS  설정 


  Next.js 프록시 (rewrites/redirects)
  - ✅ 개발 환경에서만 작동 (next dev)
  - ✅ 클라이언트 → Next.js 서버 → Spring 백엔드 구조
  - ✅ CORS 이슈를 개발 중에는 가립니다

  프로덕션 환경
  - ❌ Next.js 프록시가 작동하지 않음
  - ❌ 브라우저가 직접 Spring에 요청
  - ✅ Spring의 CORS 설정이 필수

  개발 (next dev):
  브라우저 → http://localhost:3000/api → Next.js 프록시 → Spring

  프로덕션:
  브라우저 → https://example.com/api → 직접 Spring 요청 (CORS 필요)

  Spring CORS 설정 예시

  @Configuration
  public class CorsConfig {
      @Bean
      public WebMvcConfigurer corsConfigurer() {
          return new WebMvcConfigurer() {
              @Override
              public void addCorsMappings(CorsRegistry registry) {
                  registry.addMapping("/api/**")
                      .allowedOrigins("https://example.com")
                      .allowedMethods("GET", "POST", "PUT", "DELETE")
                      .allowCredentials(true);
              }
          };
      }
  }

  CQRS는?

  CQRS(Command Query Responsibility Segregation)는 완전히 다른 아키텍처 패턴입니다:
  - 읽기(Query)와 쓰기(Command)를 분리하는 것
  - 프록시/CORS와는 무관

  따라서 프로덕션 배포 시에는 반드시 Spring CORS 설정을 해야 합니다.
  ⎿  Stop says: Hookify import error: No module named 'hookify'

---

frontend, backend 


  방식 1: 별도 컨테이너 + CORS (가장 단순)

  # docker-compose.yml
  services:
    frontend:
      image: frontend:latest
      ports:
        - "3000:3000"
      environment:
        NEXT_PUBLIC_API_URL: http://backend:8080

    backend:
      image: backend:latest
      ports:
        - "8080:8080"


방식 2: Nginx 리버스 프록시 (권장) ⭐

  # docker-compose.yml
  services:
    nginx:
      image: nginx:latest
      ports:
        - "80:80"
      volumes:
        - ./nginx.conf:/etc/nginx/nginx.conf

    frontend:
      image: frontend:latest
      expose:
        - "3000"

    backend:
      image: backend:latest
      expose:
        - "8080"

  # nginx.conf
  upstream frontend {
      server frontend:3000;
  }

  upstream backend {
      server backend:8080;
  }

  server {
      listen 80;
      server_name localhost;

      location / {
          proxy_pass http://frontend;
      }

      location /api/ {
          proxy_pass http://backend;
      }
  }

  장점:
  - ✅ 같은 도메인 (localhost)에서 작동
  - ✅ CORS 설정 불필요
  - ✅ next.config.js 프록시도 필요 없음

---

깃 사내설치.  - 연구소 망에서 접속가능한 곳으로

items(id) -> Blue_print(externalId) -> CatalogVersion
URL 형태 ->  "externalId": "/blueprint/api/blueprints/d935f187-ecaa-4494-8175-2692ad46c121" (blueprint는 버전이 있고(주기적인 업데이트를 가정함), workflow는 버전이 없음)
UUID 형태 -> "externalId": "f4264fae-ca2a-4380-97c6-b6e909df4a20",

비교 
1.Catalog 목록을 가져온다.
2.DB에 저장된 lastUpdatedAt 보다 최신인 Blueprint 아이템만 선별한다.
3.변경된 아이템에 대해서만 externalId를 통해 버전을 가져온다,

---

- https://vmapps.gooddi.lab/blueprint/api/blueprints?$top=3000
- blueprint만 가져온다

장점 - 휴식을 안함. 
대신에 - 돈을 더받음

- 6월 3일까지 쉰다고 가정했을떄 
- 연차를 다 소진한다면 
---

Cluster 시스템/인프라 단위, 여러 대의 서버(Node)를 하나로 묶은 컴퓨터 집합
Namespace 논리적 분리 단위, 클러스터 안에서 팀별로 자원을 나누는 폴더, 노드는 공유한다.
Node 물리적 단위, 실제 컨테이너가 돌아가는 한 대의 서버 
Pod 최소 배포 단위, 쿠버네티스가 관리하는 가장 작은 단위 






- VCF 이정원 선임님, 파일이관 여부 체크기 




1.Pod ->  pvc- >  PV (기본적으로 선택하지 않음.)
2.PV -> Pod 

PV , Storage Class  300GB 
pvc pv는 1대1대응이다. 명세서와 영수증 

- provision 
- pvc PV (30GB)

node
- tanzu Good 

prometheus
- 
