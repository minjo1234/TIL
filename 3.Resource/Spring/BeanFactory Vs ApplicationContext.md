
### BeanFactory

- 스프링 컨테이너의 최상위 인터페이스이다.
- 스프링빈을 관리하고 조회하는 역할을 담당한다.
- getBean()을 제공한다.

### ApplicationContext
- BeanFactory 기능을 모아 상속받아서 제공한다.
- 애플리케이션을 개발할 때는 빈을 관리하고 