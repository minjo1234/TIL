

- ConCurrentHashMap vs Redis 





---
### Spring - Redis 사용법 

> buidl.gradle 세팅 
```gradle
implementation group: 'org.springframework.boot', name: 'spring-boot-starter-data-redis', version: '3.3.0' 
```

사용법 : @Cacheable vs RedisTemplate 

@Cacheable 선언적 캐싱  

**장점**

- 간결하게 캐시를 제어할 수 있다.
- Spring이 자동으로 캐시를 관리한다.
- 비즈니스 로직과 캐싱의 분리 

**단점**

- 조건부 캐싱이 복잡하다.
- 캐시가 있는지 없는지 체크가 어렵다 - ?

그럼 언제 @Cacheable을 사용할까 ?

- 단순 조회 결과 캐싱 - @Cacheable 
- 캐시 체크 등 캐시관련 로직 존재 시 - RedisTemplate를 이용한다.


Redis에서 데이터를 가져올때는 LinkedHashMap으로 역직렬화 된다.
타입정보를 같이 저장시켜 직렬화시 객체로 받아들인다.

---
### Docker-Compose 구성

```yaml 

redis:
    image: redis:7-alpine
    container_name: redis
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    command: >
      redis-server
      --appendonly yes
      --maxmemory 2gb
       --maxmemory-policy allkeys-lru
    restart: unless-stopped
    networks:
       - net
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 3s
      retries: 3
      
  # Redis Commander - GUI 관리 도구 (선택사항, 개발 환경에서만 사용 권장)
  redis-commander:
    image: rediscommander/redis-commander:latest
    container_name: redis_commander
    environment:
      - REDIS_HOSTS=local:redis:6379
    ports:
      - "8082:8081"
    depends_on:
      - redis
    restart: unless-stopped
    networks:
      - net
    profiles:
      - dev  # 개발 환경에서만 실행
```



### Docker 실행 명령어 - local 

> redis 
> 
```
docker run -d \
  --name redis 
  --network net \
  -p 6379:6379
```

 > redis-commander 
```
docker run -d \
  --name redis_commander \
  --network net \
  -p 8082:8081 \
  -e REDIS_HOSTS=local:redis:6379 \
  rediscommander/redis-commander:latest
```


---

