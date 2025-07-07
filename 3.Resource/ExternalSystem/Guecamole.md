### 도입 배경


### 나의 상황 

- VPC(Virtual Public Cloud)에 분산된 VM에 사용자들이 원격으로 접근하고자 하는 요구사항 이 발생하여 도입 
- 각 VM은 **Transit Segment** 같은 내부망에만 붙어 있어서 외부에서 직접 접근할 수 없음.
- VM마다 SSH/RDP 접속이 필요하지만, 사용자가 직접 내부망 구조나 IP를 알게 하고 싶지 않음. 
- 포털(관리 서버)이 대신 Guacamole 서버랑 연동해서 사용자가 **웹 브라우저만으로 콘솔(터미널/데스크탑)**을 띄울 수 있게 하고 싶음.
- VM마다 포트포워딩이 되어 있더라도, 이걸 사용자가 직접 연결하지 않고 **중앙 게이트웨이로 통합 관리**하고 싶음.
- 따라서 **사용자 쪽에 별도 클라이언트 설치 필요 없이, 보안 제어된 게이트웨이로 내부망을 안전하게 오픈**하는 역할로 Guacamole이 필요함.

---

### 도입 이유

**왜 Guacamole을 도입했는가?**

- 우리 인프라는 여러 VPC에 VM과 클러스터가 분산되어 있고, 이 VM들은 Transit Segment(내부망)으로만 연결된다.
- 일반 사용자에게는 직접 내부망 접근 권한을 주지 않고, 포털에서 인증과 연결을 대신 관리해야 한다.
- VM에 접근하기 위해 SSH, RDP 등 다양한 원격 접속 방식이 필요하지만, 사용자 환경에 클라이언트 프로그램을 설치하게 하고 싶지 않았다.
- Guacamole을 도입해 웹 브라우저만으로 터미널/데스크탑에 접속할 수 있게 하고, 외부에서 직접 내부망을 노출하지 않고도 포털을 통해 안전하게 접근할 수 있도록 했다.
- 이를 통해 포트포워딩과 NAT 설정을 중앙 집중적으로 관리하고, 접근 권한과 세션을 포털에서 제어하며 보안성을 유지할 수 있다.

---

```scss
 ┌────────────┐       ┌───────────────┐       ┌────────────┐
 │   Portal   │ <---> │  Guacamole     │ <---> │    VM      │
 │ (Admin UI) │       │ (Terminal Proxy) │     │ (Linux etc)│
 └────────────┘       └───────────────┘       └────────────┘
         │
   (Same Subnet / Same VPC)

```

- **포탈**은 Guacamole에 API 호출만 함 (토큰 생성, 세션 관리)
- **Guacamole 서버**는 VM으로 SSH 연결 Proxy 역할.
- **VM**은 Private IP만 가지고 있음 (Public IP 불필요).
- 이 3개가 같은 서브넷(VLAN, Subnet, VPC 세그먼트 등) 안에 있으면,
    - Guacamole → VM 으로 **내부망 SSH** 가능.
    - 방화벽만 열려 있으면 됨.
- 외부에서 접근은 포탈(또는 Guacamole)에만 HTTPS로.
---


## ✅ 이런 식이면 좋은 점 (장점)

- **Public IP 할당 비용 없음** → 대량 VM 운영 시 비용↓
- SSH 직접 노출 안됨 → 보안↑
- Bastion 따로 두는 것보다 구조 단순 (Guacamole 자체가 Bastion 역할)


## 단점

### 보안 리스크

- 네트워크 경계가 좁아짐 → 보안 리스크  (누구든 같은 서브넷에 있으면 내부 IP로 곧장 접근 가능)
- 특히 Guacamole 서버가 해킹되면 → 같은 세그먼트의 VM들도 모두 노출됨.
- ACL, Security Group, 방화벽 정책이용하여 이를 해결

---
### 수평 확장 어려움

- VM이 많아지면 Guacamole가 같은 세그먼트에 계속 붙어야 하고,
- Guacamole 서버도 늘어나면 **Load Balancer + 여러 대 Guacamole + SSH Proxy** → 네트워크 설계가 복잡해짐.

---

## ✅ 4️⃣ 외부에서 직접 붙을 수 없음

- Private IP 기반이라 Guacamole 서버가 반드시 Proxy 역할을 해야 함.
- Guacamole 서버가 죽으면 터널링 자체가 끊김 → SSH 접근 단일 장애지점(SPOF).
- 그래서 실무에선 Guacamole HA(다중 서버 + Sticky Session + DB Cluster) 같이 운영.

->  맞아요! 핵심이 **모든 VM에 Public IP를 무조건 붙일 필요는 없다**는 거니까,
- 중요한 VM 몇 개만 AIP 붙여서 **직접 SSH fallback 경로 확보** → 단일 장애지점 보완.
- 이건 클라우드 비용/보안 밸런스 잘 잡는 실무 방식이에요.


## 5️⃣ 네트워크 트래픽 모니터링/감사 필요

- 내부 SSH 터널링은 외부 로깅이 어려움.
- 누가 어떤 VM에 붙었는지 Guacamole Audit + 로그 서버로 중앙화 안 하면 추적 불가.
- 실무에선 Guacamole Session Logging Plugin, SSH Session Record 따로 붙임.

-> 
### ✅ 5️⃣ 트래픽 모니터링/감사 → 지금이 도입 타이밍

- 정말 맞아요.
- `Guacamole`은 자체 Audit Log도 있고,  
    DB(예: MariaDB)로 Session 기록 가능.
- 여기에 중앙 로그(ELK, Splunk) 붙이면 **누가 언제 어디 접속했는지 추적** 가능.
- SSH 세션 레코딩은 Guacamole로는 기본 제공 안 되니 → `ttyrec`, `auditd` 같이 써도 좋고.