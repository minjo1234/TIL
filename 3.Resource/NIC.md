
✅ **NIC(Network Interface Card, 네트워크 어댑터)**는 VM이나 서버에 **여러 개를 붙일 수 있습니다.**  
가상화 환경(VMware, KVM, OpenStack, AWS VPC 등)에서는 **vNIC(Virtual NIC)**라고도 부르죠.


1️⃣ VPC는 가상 네트워크라서 Peering 없이도 다른 VPC와 자동으로 통신할 수 있다. ( O / X )  
2️⃣ 하나의 NIC는 동시에 두 개 이상의 서로 다른 서브넷에 연결될 수 있다. ( O / X )  
3️⃣ VM이 여러 네트워크에 붙으려면 NIC를 여러 개 추가해야 한다. ( O / X )  
4️⃣ Transit Segment는 VPC 간 내부 통신을 위해 쓰인다. ( O / X )  
5️⃣ 포털 VM이 Public Subnet에만 NIC가 붙어 있으면 Transit Segment에 있는 VM과 직접 통신할 수 있다. ( O / X )  
6️⃣ NAT는 내부 IP와 외부 IP를 서로 매핑해주는 역할을 한다. ( O / X )  
7️⃣ NIC 자체가 내부 IP를 외부 IP로 변환해주는 기능을 한다. ( O / X )  
8️⃣ 포털 VM에 Transit Segment를 붙인 NIC가 있으면, Peering VM과 직접 통신할 수 있다. ( O / X )  
9️⃣ 일반 사용자는 Transit Segment에 직접 연결되어 있지 않으면 내부 VM에 직접 접근할 수 없다. ( O / X )  
🔟 포털 VM에 여러 NIC를 붙이는 것은 보안을 위해 최소화하는 것이 좋다. ( O / X )



|번호|사용자의 답|정답|해설|
|---|---|---|---|
|1|❌|❌|맞아요! VPC는 Peering이 있어야만 서로 통신 가능.|
|2|❌|❌|맞아요! 하나의 NIC는 동시에 하나의 세그먼트/서브넷에만 붙음.|
|3|✅|✅|맞아요! 여러 네트워크에 붙으려면 NIC 여러 개 필요.|
|4|✅|✅|맞아요! Transit Segment = VPC Peering 용도로 쓰임.|
|5|❌|❌|맞아요! Public NIC만 있으면 Transit Segment VM과 직접 통신 불가.|
|6|❓|✅|정답은 O. NAT는 내부 IP ↔ 외부 IP 변환 역할 맞습니다!|
|7|❌|❌|맞아요! NIC 자체는 변환 안 함. 변환은 NAT 게이트웨이가 처리.|
|8|❓ (O)|✅|맞아요! 포털 VM이 Transit NIC를 갖고 있으면 Peering VM과 직접 통신 OK.|
|9|✅|✅|맞아요! 일반 사용자는 Transit 세그먼트에 직접 연결되어 있지 않으면 직접 접근 못 함.|
|10|✅|✅|맞아요! NIC가 많으면 관리 복잡·보안 노출 위험, 최소화가 보안상 좋음.|

SSH, RDP, VNC 
SSH 터미널,
RDP 원격 테스크톱 
VNC 