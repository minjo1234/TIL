
## 1.인터페이스를 사용하는 상황이 존재한다고 가정해보자.   


Java 8 버전이상부터 사용가능한 확장자이다.

1.public이나 private로 method를 만드는 경우가 대게 존재하는데 
2.sessionId를 받는경우나, 상속받은 요소들은 모두 해당요소를 사용한다고 가정할 때 다시 구현해줘야하는 불편함이 존재한다.


이러한 경우에는 **default** 확장자를 사용함으로써 간편하게 해결할 수 있다.
APIcontroller를 제외한 controller 들이 BaseControllerConfig에서 유저의 아이디, 권한을 조회한다고 생각한다면 간편하게 default 확장자를 이용하여 수 많은 controller의 코드 양을 줄일 수 있다.


```java
public interface BaseControllerConfig {
	// 세션ID를 받는 메서드
	default Long getIdBySession(HttpServletRequest request) {
		return (long) request.getSession().getAttribute("userId");
	}
}


@Controller
public class TestController implements BaseControllerConfig {
	getIdBySession(request) // 구현을 하지않고도 바로 사용이 가능하다.
}
```