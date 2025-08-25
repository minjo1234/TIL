
kube-apiserver 
ETCD CLUSTER 
kube-scheduler 
Controller-Manager 
kubelet 

| **kube-scheduler** | 새로 생성된 **Pod**를 어떤 노드에 배치할지 결정.                                                                        |
| ------------------ | ------------------------------------------------------------------------------------------------------ |
| ETCD Cluster       | 쿠버네티스의 **분산 Key-Value 저장소**. 클러스터의 상태(State)와 메타데이터를 영구 저장. API 서버만 etcd와 직접 통신 가능.                    |
| **kube-apiserver** | 쿠버네티스의 **중앙 관문(API 게이트웨이)**. 모든 요청(사용자, kubelet, 컨트롤러 등)이 반드시 거치는 HTTP API 서버. 상태 조회·변경은 여기서만 가능.      |
| **kubelet**        | 각 노드에서 동작하는 **에이전트**. API 서버로부터 “이 노드에서 이런 Pod 실행해라”라는 지시를 받고 컨테이너 런타임을 통해 실행·모니터링. 상태를 다시 API 서버에 보고. |
| kube-proxy         |                                                                                                        |

---

TLS 부트스트랩 

---

- pod establishs a relationship to container 
	one to one

multi-container pods 



Cluster - Node 



---



`kubectl run nginx --image nginx`

`kubectl create -f pod-definition.yml`


Docker hub - image stroe 