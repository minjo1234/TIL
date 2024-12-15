
객체의 생성과 초기화를 분리하자는 규칙이 존재하기에 의존관계 주입이 완료된 이후에 스프링 빈의 라이프사이클 중에서 
초기화 콜백 - afterPropertiesSet 초기화를 잉ㅇ
소멸전 콜백 - destroy 

---

**초기화, 소멸 인터페이스의 단점**
- 이 인터페이스는 스프링 전용 인터페이스, 해당 코드가 스프링 전용 인터페이스에 의존한다.
- 초기화, 소멸 메서드의 이름을 변경할 수 있다.
- 내가 코드를 고칠 수 없는 외부 라이브러리에 적용할 수 없다.

인터페이스로 상속하는 방법은 스프링 초창기 방식이고 현재는 사용하지 않는다.

----


```java

	- 의존관계 주입전에 
@Override  
public void afterPropertiesSet() throws Exception {  
    System.out.println("NetworkClient.afterPropertiesSet");  
    connct();  
    call("초기화 연결 메시지");  
}  
  
@Override  
public void destroy() throws Exception {  
    System.out.println("NetworkClient.destroy");  
    System.out.println("NetworkClient disconnect" + url);  
  
}

```