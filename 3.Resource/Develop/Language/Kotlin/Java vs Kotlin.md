
### Access Control 

### Java 

```java
// 기본 접근 제한자는 "package private" (패키지 내부에서만 접근 가능)
class MyClass {
	int field;
	void method() {}
}
```

```kotlin
// 기본 접근 제한자는 "public" (어디서든 접근 가능)
class MyClass {
	var field: Int = 0  // public
    fun method() { }     // public
}
```


### 여기서 말하는 패키지의 범위란 ? 

