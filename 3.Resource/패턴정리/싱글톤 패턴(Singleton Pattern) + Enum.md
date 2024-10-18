	 

> **싱글톤 패턴**은 <font color="#b2a2c7">**클래스의 인스턴스를 단 하나만 생성하도록 보장**하고,</font> 그 인스턴스에 접근할 전역적인 접근점을 제공하는 디자인 패턴입니다.


> 사용하게 된 이유 : 
> 회사 내부 소스코드를 보면서 상수값을 그대로 사용하면서 조건문을 사용하게 되었는데 Enum을 사용하게 되면 이로운 점이 존재하기에 Enum을 사용하려고 하였다.


#### 사용하게 된 상세내용

회사내부 코드에 신규 기능 개발을 진행하면서 service(비즈니스 로직) 작성 부분에서 switch , if 문과 상수값을 사용하게 되는 상황이 나오게 되었는데 if문과 switch문의 잦은 사용은 코드의 확장성을 낮출 수 있었고 , 상수값은 코드의 안정성(namespace , 값이 수정되어도 재컴파일 하지 않을 시 에러가 발생할 수 있음) 을 해결하기 위해 상수값은 Enum을 사용하고자 한다.


---

# Enum을 사용하게 된 이유

## 1. Enum 전에 사용했던 것  :  **int enum 패턴**


```java
public static final int APPLE_FUJI = 1; 
public static final int APPLE_PIPPIN = 2; 
public static final int ORANGE_NAVEL = 1; 
public static final int ORANGE_BLOOD = 2;

```
``
- int enum 그룹별로 별도의 namespace를 만들어주지 않기 때문에 앞에 접두어를 따로 붙여줘야 한다
	(APPLE_, ORANGE_)-
- ORANGE_를 인자로 받을 메서드에 APPLE_을 인자로 넘겨도 문제없이 동작한다. 의도와는 다르게 동작.
- **컴파일 시점 상수**이기 때문에 상수를 사용하는 클라이언트 코드와 함께 컴파일된다. **상수값이 변경되면 클라이언트도 다시 컴파일** 해야한다. 

-> _**프로그램이 깨지기 쉽다.**_


### 2.문제점 예시

2-1 네임스페이스 부족 : 타입이 달라도 에러를 발견하지 못 할 수 가 있다.
- APPLE_FUJI 대신에 ORANGE_NAVEL을 사용해도 에러를 발견하지 못 할 수 있음 


```java
public static final int APPLE_FUJI = 1; 
public static final int APPLE_PIPPIN = 2; 
public static final int ORANGE_NAVEL = 1; 
public static final int ORANGE_BLOOD = 2;
```


```java
public class FruitHandler {
    public void handleApple(int appleType) {
        if (appleType == APPLE_FUJI) {
            System.out.println("Handling Fuji Apple");
        } else if (appleType == APPLE_PIPPIN) {
            System.out.println("Handling Pippin Apple");
        } else {
            System.out.println("Unknown Apple Type");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        FruitHandler fruitHandler = new FruitHandler();
        fruitHandler.handleApple(ORANGE_NAVEL); // 잘못된 타입의 값을 전달하지만 컴파일러는 오류를 잡아내지 못합니다.
    }
}
```

2-2 상수값 변경 시 클라이언트 코드 재컴파일 필요
- 컴파일을 하지 않을 시 1이 출력될 수 있다는 단점이 존재함

```java
public static final int APPLE_FUJI = 1;
public static final int APPLE_PIPPIN = 2;
```

```java
// 상수값 변경 전
public static final int APPLE_FUJI = 1;
public static final int APPLE_PIPPIN = 2;

public class Main {
    public static void main(String[] args) {
        System.out.println(APPLE_FUJI); // 1 출력
    }
}

// 상수값 변경 후
public static final int APPLE_FUJI = 3; // 변경됨
public static final int APPLE_PIPPIN = 2;

public class Main {
    public static void main(String[] args) {
        System.out.println(APPLE_FUJI); // 3 출력되어야 하지만 1이 출력될 수 있음 (컴파일하지 않은 경우)
    }
}
```



---

#### <font color="#b2a2c7"> 이로운 점 </font>

```java
public enum FruitType {
    APPLE_FUJI,
    APPLE_PIPPIN,
    ORANGE_NAVEL,
    ORANGE_BLOOD
}

public class FruitHandler {
    public void handleApple(FruitType appleType) {
        if (appleType == FruitType.APPLE_FUJI) {
            System.out.println("Handling Fuji Apple");
        } else if (appleType == FruitType.APPLE_PIPPIN) {
            System.out.println("Handling Pippin Apple");
        } else {
            System.out.println("Unknown Apple Type");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        FruitHandler fruitHandler = new FruitHandler();
        fruitHandler.handleApple(FruitType.ORANGE_NAVEL); // 컴파일 오류 발생: 잘못된 타입
    }
}  // (enum 자료형이 **동일성 비교(==)가 가능**한 이유가 서로 싱글톤 객체이기 때문)
```



enum 을 사용하면 조건문을 

> 1.namespace제공 및 싱글톤 패턴으로 비교가 이로움

- 자바의 enum 자료형은 완전한 기능을 갖춘 클래스로, 다른 언어의 enum보다 강력하다.
- enum의 기본적 아이디어는, **열거 상수별로 인스턴스를 만들어 public static final 필드 형태로 제공**하는 것이다.
- enum 자료형은 사실상 **final으로 선언된 것이나 마찬가지**인데, **접근 가능한 생성자가 아예 없기 때문**이다.
- enum 자료형으로 새로운 객체를 생성하거나, 상속을 통한 확장을 할 수 없기 때문에 이미 선언된 enum 상수 이외의 객체는 사용할 수 없다.
- = **사실상** **싱글톤과 같다.** 아니 사실상이 아니고 그냥 싱글톤이다.**싱글톤을 일반화한 형태.**

----

> 2. 컴파일 시 안정성 보장 
* enum 자료형은 **컴파일 시점 형 안전성을 보장**한다. 
- Apple 형의 인자를 받는다고 선언한 메서드는 반드시 Apple 자료형에 속한 값만 받는다. 다른 자료형을 넣으려고 하면 컴파일 시점에서 오류가 발생한다. (== 비교도 마찬가지)


---

> **이후 확인해볼점** 

1.fromString :  **toString으로 뱉어내는 문자열을 가지고 다시 enum 객체로 변환**할 수 있는 **fromString 메서드** 제공을 고민해봐라

2.enum 자료형은 임의의 메서드나 필드도 추가할 수 있고, 심지어 임의의 인터페이스를 구현할 수도 있다.

3.enum 자료형은 이미 **Object**에 정의된 모든 메서드들이 포함되어 있으며, **Comparable, Serializable** 인터페이스는 **이미 구현이 되어있다**


** 사용하면서 여러번 정독해야할듯 ** 

---

참조 :

1.상수 대신 Enum을 사용해라  : https://sedangdang.tistory.com/240





```java
```