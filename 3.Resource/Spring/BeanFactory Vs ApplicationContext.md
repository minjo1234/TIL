
### BeanFactory

- 스프링 컨테이너의 최상위 인터페이스이다.
- 스프링빈을 관리하고 조회하는 역할을 담당한다.
- getBean()을 제공한다.

### ApplicationContext
- BeanFactory 기능을 모아 상속받아서 제공한다.
- 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능은 물론이고, 수 많은 부가기능이 필요하다.


ApplicationContext
- MessageSource - 한국어로 들어오면 한국어로, 영어권으로하면 영어
- EnviormentCapable - 로컬, 개발, 운영등을 구분해서 관리 
- ApplicationEventPublisher - 이벤트를 발생하고, 구독하는 모델을 편리하게 관리
- ResourceLoader - 파일 클래스패스 외부 등에서 리소스를 편리하게 조회