

- ConCurrentHashMap vs Redis 







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

