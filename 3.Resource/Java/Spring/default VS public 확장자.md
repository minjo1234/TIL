
## 1.인터페이스를 사용하는 상황이 존재한다고 가정해보자.


1.public이나 private로 method를 만드는 경우가 대게 존재하는데 
2.sessionId를 받는경우나, 상속받은 요소들은 모두 해당요소를 사용한다고 가정할 때 다시 구현해줘야하는 불편함이 존재한다.


이러한 경우에는 **default** 확장자를 사용함으로써 간편하게 해결할 수 있다.
API

```java
public interface BaseControllerConfig 
```