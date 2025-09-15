
```java

// 추상 클래스 (공통 메서드 + 추상 메서드)
public abstract class AbstractMailSender<T> {

// 공통 로직 (Template Method)
public void sendMail(T parameter) {
EmailSendingInfo emailSendingInfo = createEmailSendingInfo(parameter);
producer.produce(new SendEmailEvent(emailSendingInfo, 0L, ownerFinder, null));
}

// 하위에서 구현할 추상 메서드들
protected abstract Map<String, Object> createTemplateModel(T parameter);
protected abstract EmailSendingInfo createEmailSendingInfo(T parameter);
}

  

// 구현체들
public class FindMyIdMailSender extends AbstractMailSender<User> {

@Override
protected Map<String, Object> createTemplateModel(User user) { }
@Override
protected EmailSendingInfo createEmailSendingInfo(User user) { }
}

```

### 상위 클래스(추상 클래스)






--------
### 하위 클래스들 
