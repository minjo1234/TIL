
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

critcl exec -i -t 

criticl logs 
```