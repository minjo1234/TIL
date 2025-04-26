
"무언가를 가로채다" 라는 의미를 가집니다.
시점은 컨트롤러에 접근하기 전과 후로 나뉩니다.

1. 내가 궁금했던 점은 preHandle 같은 메서드를 사용하면 session 값 등을 설정해줄수 있는데 해당 값을 클라이언트 쪽에서 어떻게 사용이 가능한지가 궁금했다.
2. 프로젝트에서는 Thymeleaf 템플릿 엔진을 사용하고 있었고(SSR - 서버 사이드 렌더링 : 서버에서 데이터를 처리한 이후 HTML을 렌더링하고, 완성된 HTML페이지가 클라이언트에 전달된다.)  

```java
@Override  
public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {  
    HttpSession session = request.getSession();  
    Long userId = (Long) session.getAttribute("userId");  
    User userByUserId = userRepository.findUserByUserId(userId);  
    session.setAttribute("userName", userByUserId.getName());  
    session.setAttribute("role", userByUserId.getUserRoleType());  
    session.setAttribute("contextPath", request.getServletContext().getContextPath());  
    return true;  
}
```

### 1.HandlerInterceptor 를 이용하여 Interceptor 구현하기

### 2. **WebMvcConfigurer** 인터페이스 구현하기.



https://congsong.tistory.com/24

...minjoVue.user.filter(u  => u.id + '' == value)[0]

