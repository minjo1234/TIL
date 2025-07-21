
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