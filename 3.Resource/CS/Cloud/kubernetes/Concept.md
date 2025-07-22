
kubernetes is a orchestarion platform that helps you distribute and operate multiple containers efficiently. The system consists largely of a **Master Node** and multiple **Worker Node** 

---

## **🧠 Master Node (Control Plane)**

The Master Node is the brain of the kubernetes cluster. It manages and controls the entire system - **scheduling workloads, maintaining cluster state, and handling updates.**

- **API Server**: The front door of the cluster. All commands (like kubectl) interact with the API server.
    
- **Scheduler**: Decides _which_ Pod runs on _which_ Worker Node based on resources and rules.
    
- **Controller Manager**: Watches the cluster and ensures that the actual state matches the desired state (e.g., restarts crashed Pods).
    
- **etcd**: A distributed key-value store. It stores the cluster’s configuration and current state.

---

## **🛠️ Worker Node**

The **Worker Node** is where the actual work happens. It runs the **Pods** (which hold your containers) and reports back to the Master.

- **kubelet**: An agent that receives tasks from the Master and runs Pods accordingly.
    
- **kube-proxy**: Handles networking, making sure traffic reaches the right Pod.
    
- **Container Runtime**: The actual software that runs containers (e.g., Docker, containerd).

----

## Ctr 


ctr stands for Container Runtime CLI, and it is the command-line interface for containerd, a popular container runtime.


- Pull container images 
- Run containers 
- Inpsect, pause, or stop container 
- Manage namespace and snapshots 


---

## dockered (Docker Daemon)


consists of 
- containerd 
- builkdkit 
- network, volume, api server

## Containerd 

containered is a container runtime a core piece of software that runs containers 


[사용자]
   ↓
docker CLI
   ↓
dockerd (Docker Daemon)
   ↓
containerd
   ↓
runc
   ↓
[실제 컨테이너 실행]



### General docker use flow 

# 사용자는 docker CLI 사용
docker run nginx

# 내부 동작
→ docker CLI  
→ dockerd (Docker Daemon)  
→ containerd  
→ runc  
→ 실제 컨테이너 실행

---

### nerdctl 

# Docker 없이도
nerdctl run nginx

# 내부 동작
→ nerdctl CLI  
→ containerd  
→ runc  
→ 실제 컨테이너 실행


---

crictl 

```
crictl 

crictl pull busybox 

crictl images 

crictl exec -i -t 

crictl logs 

crictl pods
```

---

|**항목**|kubectl|crictl|
|---|---|---|
|목적|Kubernetes 클러스터 전체 관리|개별 노드의 컨테이너 런타임 디버깅|
|사용 대상|API 서버 → 클러스터 리소스 (Pod, Node, etc.)|노드의 container runtime (containerd, cri-o)|
|연결 대상|Kubernetes API 서버|노드의 CRI 소켓 (/run/containerd/containerd.sock 등)|
|용도|애플리케이션 배포, 상태 확인 등|Pod 내부 컨테이너 디버깅, crash 원인 확인 등|
|레벨|클러스터 수준|노드 수준 (kubelet 밑)|


```bash
kubectl get pods
kubectl logs my-pod
kubectl describe pod my-pod
kubectl exec -it my-pod -- /bin/sh
```

```bash
crictl ps
crictl inspect <container-id>
crictl logs <container-id>
crictl exec -it <container-id> /bin/sh
```


ctr vs nodectl vs crictl 


---

### Docker deprecated 

## **🧭 무엇이 deprecated 되었는가?**


Kubernetes는 **Docker 자체를** deprecated한 게 아니라,

**Kubelet이 Docker를 직접 사용하는 기능(DockerShim)**을 deprecated하고 제거했습니다.

- 🔧 **기존:**
    
    Kubelet이 내부적으로 Docker를 직접 호출하여 컨테이너 관리
    (dockershim 사용)
    
- 🔄 **이후:**
    
    Kubelet은 **Container Runtime Interface(CRI)** 를 사용해서
    **containerd나 CRI-O 같은 런타임**과 통신

---

|                  |           |                                  |
| ---------------- | --------- | -------------------------------- |
| kubectl 사용       | ❌ 없음      | 그대로 사용 가능                        |
| Dockerfile / 이미지 | ❌ 없음      | 여전히 docker build, docker push 가능 |
| 컨테이너 실행          | ⚠️ 일부 있음  | 노드에서 docker 대신 containerd 사용     |
| 노드에 Docker 설치    | ❌ 권장되지 않음 | 더 이상 필요 없음 (containerd 사용 권장)    |


### **🔴 과거 방식 (deprecated)**

Kubelet → Dockershim → Docker → containerd → runc

### **✅ 현재 방식 (권장)**

Kubelet → CRI → containerd → runc

---


## **💡 대체 방안**

- **개발:** docker는 그대로 써도 됨 (docker build, docker push)
- **운영 (Kubernetes 노드):** containerd or CRI-O 사용
- **디버깅:** crictl, nerdctl (containerd-friendly CLI) 사용



----


rkt(발음: _로켓_, 과거 명칭: CoreOS Rocket)는 **컨테이너 런타임(runtime)** 중 하나였습니다. 하지만 **현재는 더 이상 유지되지 않으며, 공식적으로 deprecated 상태**입니다.



-----------





- 소프트웨어 추가설치 deprecated 
- dns 
- vm명 규칙
- dash board 항목 db에서 

테스트 케이스 어떻게 만들것인지 구상해보기


---

### Docker vs Containerd 


crictl 

- **주 용도**: Kubernetes 노드에서 컨테이너 상태 확인, 디버깅, 이미지 확인 등
- Kubernetes는 **CRI(Container Runtime Interface)** 를 통해 컨테이너 런타임과 통신합니다.

CRI 호환 런타임이다.
docker는 더 이상 Kubernetes의 기본 런타임이 아니며, 대신 **containerd**나 **CRI-O**를 사용합니다.


Kubernetes는 **CRI(Container Runtime Interface)** 라는 표준 인터페이스를 통해 다양한 컨테이너 런타임을 지원하는 구조예요.

### **🧩 원래 구조 (과거: Docker 사용 시)**

```
Kubernetes (kubelet)
     ↓
dockershim (중간 번역기)
     ↓
Docker Engine
     ↓
containerd → runc → 실제 컨테이너 실행
```


```
Kubernetes (kubelet)
     ↓
CRI
     ↓
containerd (또는 CRI-O)
     ↓
runc → 컨테이너 실행
```

- 지금은 Docker 없이 containerd 같은 **CRI 호환 런타임**을 Kubernetes가 직접 제어함 
- 
---


> Kubernetes에서 **컨테이너에 직접 접근하거나 디버깅할 때**,
> 일반 유저는 kubectl exec 같은 명령어를 주로 쓰고,
> 시스템 레벨에서 **노드 내부에서 직접 접근**할 땐 crictl을 사용합니다.


---

## **🔍 1.** ## **접근 경로 (계층 구조)**


| **구분** | **시스템 레벨 접근**                       | **Kubernetes 추상화 접근**                           |
| ------ | ----------------------------------- | ----------------------------------------------- |
| 도구     | crictl, nsenter, containerd, runc 등 | kubectl exec, kubectl logs                      |
| 경로     | **OS → 런타임(containerd) → 컨테이너**     | **kubectl → API Server → kubelet → 런타임 → 컨테이너** |
| 권한     | **직접 root 권한 필요**                   | Kubernetes 권한 (RBAC, Role) 필요                   |
| 사용 위치  | **노드 내부 (SSH 접속)**                  | 클러스터 외부에서도                                      |


즉, 시스템 레벨 접근은 **Kubernetes를 우회해서 직접 컨테이너를 다루는 것**이고,
kubectl은 **Kubernetes의 추상화된 API를 통해 안전하게 접근**하는 방식입니다.

## **🧱 2.** ## **실제 대상 vs 추상 리소스**

