
### Hash Map 

```java
public class HashMap<K,V> extends AbstractMap<K,V>
	implements Map<K,V>, Cloneable, Serializable {
	
		public V get(Object key) {} 
		public V put(K key, V value) {}
	}
```

Map 인터페이스를 구현한 클래스 중에서 성능이 제일 좋다. 
하지만 `synchronized` 키워드가 존재하지 않기 때문에 당연히 `Multi-Thread` 환경에서 사용할 수 없다.

