### 사용계기 

단순 Docker 만으로는 HA과 자동 복구 측면에서 한계가 존재하여 쿠버네티스 도입을 선택하였다.
오케스트레이션 (특정 서버가 죽었을 때 그 위의 컨테이너를 다른 서버로 옮겨준다.)

사용할 때의 판단과정 

- **1.무중단 배포**가 필수적이다.
- 2.서버 1대가 죽어도 서비스는 **자동으로 복구**되어야 한다.
- 3.추후에 서버(Node)를 쉽게 추가하고 싶다. - 외부



- **자가 치유(Self-healing):** 포털 컨테이너가 죽으면 K8s가 즉시 다른 건강한 노드에 다시 띄웁니다.
- **L7 로드밸런싱 (Ingress):** Nginx를 따로 관리할 필요 없이, K8s Ingress가 트래픽 분산과 SSL 인증서 처리를 표준화된 방식으로 해결합니다.


### ① 포털 & Nginx (Stateless 영역)

- **Nginx:** 별도의 서버로 두지 말고 **Ingress Controller**(예: ingress-nginx)를 사용하세요. 클러스터 진입점 역할을 하며 L7 스위칭을 담당합니다.
- **Portal (2대):** `Deployment` 객체로 관리하며 `replicas: 2`로 설정합니다. 서로 다른 노드에 배치되도록 **Pod Anti-Affinity** 설정을 추가하는 것이 이중화의 핵심입니다.

② DB & Redis (Stateful 영역)
- StatefulSet 사용:
- PVC(Persistent Volume Claim):
- 이중화 전략: * DB (MySQL/PostgreSQL): 




1.Stateless 영역이란 무엇인지 , 보통 저렇게 Stateless 영역, DevOps 영역, Stateful 영역을 나누는지 각각의 차이는 무엇인지

2.가용성과 자동복구의 차이 ? 가용성은 무엇이고 자동복구는 무엇인지.
