
마이크로커널 아키텍쳐 (microkernel / plug-in architecture)

### **코어 시스템**

- 시스템을 실행시키는 데 필요한 최소한의 기능


### **플러그인**

특정 처리 로직, 부가 기능뿐만 아니라 코어 시스템의 기능 변경을 위한 Add-on 스타일을 지원하는 standalone 컴포넌트
코어 시스템 자체를 개선/확장할 수 있는 역할을 한다는 것과 **standalone** 이어야 한다는 것이다. 즉, 다른 플러그인이 없으면 동작할 수 없는 형태가 아닌 단독 플러그인으로써의 동작을 보장해야한다는 것이다.
일반적으로 플러그인은 코어시스템과 point-to-point 관계이며, 따라서 대부분의 연결고리는 entry-point class를 호출해주는 메서드나 함수이다.



StandAlone ? 
point-to-point 란 
entry-point class 
runtime-based  plugin-add one 방식말고 다른것도 있나 찾아보자.

