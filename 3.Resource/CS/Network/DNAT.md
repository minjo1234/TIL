
Destination Network Address Translation 
목적지 IP 주소를 변환하는 네트워크 기술 


### 왜 씀 ?

외부 공개용 IP가 제한적인 상황에서 
하나의 외부 IP -> 내부에서 분기되는 구조를 이용한다.

- **외부 IP**는 하나인데, 사용자의 요청 **속성**(권한, 경로, 포트, 헤더 등)에 따라
- 방화벽이나 프록시(또는 로드밸런서)가 요청의 **목적지**를 바꿔서
- 각각 다른 **내부 서버/서비스**로 라우팅해 줍니다.


```
[외부 사용자] → [공인 IP:80] → [방화벽 DNAT] → [내부 서버 10.0.0.5:8080]
```



Transit Address = 연결 주소 = 
