
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
type Language = 'ko' | 'en'; 

2.인터페이스 정의 
```
```
interface LanguageContextType {  
  language: Language;  
  setLanguage: (lang: Language) => void;  
  toggleLanguage: () => void;  
}



  왜 필요한가?
  - TypeScript 타입 안정성 확보
  - IDE 자동완성 지원
  - 실수 방지 (예: setTheme('red') → 컴파일 에러)

  ---
  ✅ 2단계: createContext 생성

  목적: React Context 저장소 생성

  // ③ Context 생성
  const ThemeContext = createContext<ThemeContextType | undefined>(undefined);
  //                                                    ↑↑↑↑↑↑↑↑↑
  //                  초기값 undefined (Provider 없으면 에 러 발생시키기 위함)

  왜 undefined로 초기화?
  // ❌ 잘못된 방법: 기본값 제공
  const ThemeContext = createContext<ThemeContextType>({
    theme: 'light',
    setTheme: () => {},
    toggleTheme: () => {}
  });
  // → Provider 없이 사용해도 에러 안남 (위험!)

  // ✅ 올바른 방법: undefined
  const ThemeContext = createContext<ThemeContextType | undefined>(undefined);
  // → Provider 없으면 에러 발생 (안전!)

  ---
  ✅ 3단계: Provider 컴포넌트 작성

  목적: 전역 상태와 로직을 관리하고 제공

  // ④ Provider 컴포넌트
  export function ThemeProvider({ children }: { children: ReactNode }) {
    // ④-1. 상태 정의
    const [theme, setThemeState] = useState<Theme>('light');

    // ④-2. 초기화: localStorage에서 불러오기
    useEffect(() => {
      const savedTheme = localStorage.getItem('theme') as Theme;
      if (savedTheme === 'light' || savedTheme === 'dark' || savedTheme === 'auto') {
        setThemeState(savedTheme);
      }
    }, []);

    // ④-3. 테마 설정 함수 (localStorage 저장 포함)
    const setTheme = useCallback((newTheme: Theme) => {
      setThemeState(newTheme);
      localStorage.setItem('theme', newTheme);
    }, []);

    // ④-4. 테마 토글 함수
    const toggleTheme = useCallback(() => {
      setTheme(theme === 'light' ? 'dark' : 'light');
    }, [theme, setTheme]);

    // ④-5. Context 값 메모이제이션
    const value = useMemo(
      () => ({ theme, setTheme, toggleTheme }),
      [theme, setTheme, toggleTheme]
    );

    // ④-6. Provider로 하위 컴포넌트에 값 제공
    return (
      <ThemeContext.Provider value={value}>
        {children}
      </ThemeContext.Provider>
    );
  }

  각 단계 설명:

  | 단계 | 코드                     | 설명                                 |
  |------|--------------------------|--------------------------------------|
  | ④-1  | useState<Theme>('light') | React 상태로 테마 관 리               |
  | ④-2  | useEffect(..., [])       | 컴포넌트 마운트 시 localStorage 읽기 |
  | ④-3  | useCallback(...)         | 테마 변경 + localStorage 저장        |
  | ④-4  | useCallback(...)         | light ↔ dark 토글                    |
  | ④-5  | useMemo(...)             | 불필요한 리렌더링 방 지               |
  | ④-6  | <Provider value={...}>   | 하위 컴포넌트에 값 전달              |

  ---
  ✅ 4단계: Custom Hook 작성

  목적: useContext를 편리하게 사용할 수 있는 Hook

  // ⑤ Custom Hook
  export function useTheme() {
    const context = useContext(ThemeContext);

    // Provider 없이 사용하면 에러 발생
    if (context === undefined) {
      throw new Error('useTheme must be used within a ThemeProvider');
    }

    return context;
  }

  왜 필요한가?
  // ❌ Custom Hook 없이 사용
  import { useContext } from 'react';
  import { ThemeContext } from '@/contexts/ThemeContext';

  const context = useContext(ThemeContext);
  if (!context) throw new Error('...');  // 매번 체크 필요
  const { theme } = context;

  // ✅ Custom Hook 사용
  import { useTheme } from '@/contexts/ThemeContext';

  const { theme } = useTheme();  // 간단!

  ---
  ✅ 5단계: Root Layout에 Provider 추가

  목적: 앱 전체에서 Context 사용 가능하도록 설정

  // src/app/layout.tsx
  import { ThemeProvider } from '@/contexts/ThemeContext';

  export default function RootLayout({ children }: { children: React.ReactNode }) {
    return (
      <html lang="ko">
        <body>
          <ThemeProvider>
            {/* 이제 모든 하위 컴포넌트에서 useTheme() 사용 가능 */}
            {children}
          </ThemeProvider>
        </body>
      </html>
    );
  }

  컴포넌트 트리:
  <ThemeProvider>           ← Context 제공
    <Header>                ← useTheme() 사용 가능 ✅
      <ThemeToggle>         ← useTheme() 사용 가능 ✅
    <Main>                  ← useTheme() 사용 가능 ✅
      <BlogPost>            ← useTheme() 사용 가능 ✅
    <Footer>                ← useTheme() 사용 가능 ✅
  </ThemeProvider>

  ---
  ✅ 6단계: 컴포넌트에서 사용

  목적: 실제로 테마를 읽고 변경하기

  // src/components/ThemeToggle.tsx
  'use client';

  import { useTheme } from '@/contexts/ThemeContext';

  export default function ThemeToggle() {
    const { theme, toggleTheme } = useTheme();

    return (
      <button onClick={toggleTheme}>
        현재 테마: {theme}
        {theme === 'light' ? '🌞' : '🌙'}
      </button>
    );
  }

  ---
  ✅ 7단계 (선택): 서버 컴포넌트 지원

  쿠키 추가 (서버 컴포넌트에서 접근 가능)

  // ThemeContext.tsx 수정

  // 쿠키 헬퍼 함수 추가
  function setCookie(name: string, value: string) {
    document.cookie = `${name}=${value};path=/;max-age=31536000`;
  }

  function getCookie(name: string): string | null {
    const value = `; ${document.cookie}`;
    const parts = value.split(`; ${name}=`);
    if (parts.length === 2) return parts.pop()?.split(';').shift() || null;
    return null;
  }

  // setTheme 수정
  const setTheme = useCallback((newTheme: Theme) => {
    setThemeState(newTheme);
    localStorage.setItem('theme', newTheme);
    setCookie('theme', newTheme);  // ← 쿠키 추가
  }, []);

  // 초기화 수정
  useEffect(() => {
    const cookieTheme = getCookie('theme') as Theme;
    const localTheme = localStorage.getItem('theme') as Theme;
    const savedTheme = cookieTheme || localTheme;

    if (savedTheme === 'light' || savedTheme === 'dark' || savedTheme === 'auto') {
      setThemeState(savedTheme);
    }
  }, []);

  서버 컴포넌트에서 사용:
  // app/page.tsx (서버 컴포넌트)
  import { cookies } from 'next/headers';

  export default async function Page() {
    const cookieStore = await cookies();
    const theme = cookieStore.get('theme')?.value || 'light';

    return <div>서버에서 읽은 테마: {theme}</div>;
  }

  ---
  📦 완성된 전체 코드

⏺ Bash(cat > /tmp/ThemeContext_완성본.tsx << 'EOF'
      'use client';…)
  ⎿  Running PreToolUse hook…
  ⎿  Running…

───────────────────────────────────────────────────────────
 Bash command

   cat > /tmp/ThemeContext_완성본.tsx << 'EOF'
   'use client';

   import { createContext, useContext, useState,
   useEffect, ReactNode, useMemo, useCallback } from
   'react';

   // ============================================
   // 1️⃣ 타입 정의
   // ============================================
   type Theme = 'light' | 'dark' | 'auto';

   interface ThemeContextType {
     theme: Theme;
     setTheme: (theme: Theme) => void;
     toggleTheme: () => void;
   }

   // ============================================
   // 2️⃣ Context 생성
   // ============================================
   const ThemeContext = createContext<ThemeContextType |
    undefined>(undefined);

   // ============================================
   // 쿠키 헬퍼 함수
   // ============================================
   function setCookie(name: string, value: string) {
     document.cookie =
   `${name}=${value};path=/;max-age=31536000`;
   }

   function getCookie(name: string): string | null {
     const value = `; ${document.cookie}`;
     const parts = value.split(`; ${name}=`);
     if (parts.length === 2) return
   parts.pop()?.split(';').shift() || null;
     return null;
   }

   // ============================================
   // 3️⃣ Provider 컴포넌트
   // ============================================
   export function ThemeProvider({ children }: {
   children: ReactNode }) {
     const [theme, setThemeState] =
   useState<Theme>('light');

     // 초기화: localStorage & Cookie에서 불러오기
     useEffect(() => {
       const cookieTheme = getCookie('theme') as Theme;
       const localTheme = localStorage.getItem('theme')
   as Theme;
       const savedTheme = cookieTheme || localTheme;

       if (savedTheme === 'light' || savedTheme ===
   'dark' || savedTheme === 'auto') {
         setThemeState(savedTheme);
       }
     }, []);

     // 테마 설정 (localStorage + Cookie 저장)
     const setTheme = useCallback((newTheme: Theme) => {
       setThemeState(newTheme);
       localStorage.setItem('theme', newTheme);
       setCookie('theme', newTheme);
     }, []);

     // 테마 토글
     const toggleTheme = useCallback(() => {
       setTheme(theme === 'light' ? 'dark' : 'light');
     }, [theme, setTheme]);

     // Context 값 메모이제이션
     const value = useMemo(
       () => ({ theme, setTheme, toggleTheme }),
       [theme, setTheme, toggleTheme]
     );

     return (
       <ThemeContext.Provider value={value}>
         {children}
       </ThemeContext.Provider>
     );
   }

   // ============================================
   // 4️⃣ Custom Hook
   // ============================================
   export function useTheme() {
     const context = useContext(ThemeContext);
     if (context === undefined) {
       throw new Error('useTheme must be used within a
   ThemeProvider');
     }
     return context;
   }
   EOF
   cat /tmp/ThemeContext_완성본.tsx
