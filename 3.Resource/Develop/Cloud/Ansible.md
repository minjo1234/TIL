OS 자동화 : OS에 패키지를 설치하거나, os 환경에 대한 세팅을 해준다.

Ansible 플레이북은 **YAML**이라는 형식의 텍스트 파일로 만듭니다. 쉽게 말해 **"어떤 서버들에게(Hosts), 어떤 작업(Tasks)을 시킬 것인가"**를 순서대로 적어놓은 **작업 지시서**라고 보시면 됩니다.

###  플레이북의 기본 구조 (3요소)

플레이북은 크게 세 부분으로 구성됩니다.

1. **name:** 이 작업의 이름 (사람이 읽기 좋게)
2. **hosts:** 이 작업을 수행할 대상 서버 그룹 (예: k8s-nodes)
3. **tasks:** 실제로 수행할 명령어들의 나열

---

### Ansible 구성 

### 1. 전제 조건: `inventory.ini` 설정

먼저 접속할 서버들의 정보를 담은 인벤토리 파일입니다. (마스터 3대 구성 예시)

### 2. K3s 최적화 Ansible Playbook (`k3s_setup.yml`)

이 플레이북은 **Podman 관련 패키지를 건드리지 않고**, K3s 전용 설정과 필요한 커널 파라미터만 조정합니다.

### 3. 이 플레이북의 핵심 포인트 (RHEL 8.1 및 Podman 관련)

1. **Podman 격리:** RHEL 8은 `docker` 대신 `podman`을 사용하지만, K3s는 설치 시 `--container-runtime-endpoint`를 지정하지 않으면 내장된 **containerd**를 사용합니다. 이 플레이북은 OS의 Podman 데몬을 건드리지 않고 K3s만의 독자적인 컨테이너 엔진(containerd)을 띄우도록 설계되었습니다.
    
2. **Firewalld & SELinux:** RHEL 환경에서 쿠버네티스 통신을 가장 많이 방해하는 요소입니다. 폐쇄망 솔루션의 안정성을 위해 우선 비활성화하도록 설정했습니다. (보안 정책상 필요하다면 특정 포트만 허용하는 방식으로 수정 가능합니다.)
    
3. **Longhorn 대비:** `iscsi-initiator-utils`를 미리 설치하여, 나중에 **공유 스토리지(Longhorn)**를 바로 올릴 수 있는 환경을 만듭니다.
    
4. **HA 자동화:** 3대의 마스터 노드를 자동으로 연결하여, 한 대가 죽어도 서비스가 유지되는 **고가용성 클러스터**를 한 번에 구성합니다.'

---


정말 죄송합니다! 제가 코드를 담는 박스 기능에서 계속 오류가 났던 모양입니다. 이번에는 **특수 박스 없이 생 텍스트(Plain Text)**로 직접 적어드릴게요. 이 방식으로는 무조건 보이실 겁니다.

아래 내용을 메모장에 복사해서 각각 `inventory.ini`와 `k3s_setup.yml`로 저장하시면 됩니다.

---

### 1. inventory.ini 파일 내용

[k3s_masters] master01 ansible_host=192.168.0.101 master02 ansible_host=192.168.0.102 master03 ansible_host=192.168.0.103

[all:vars] ansible_user=root ansible_ssh_pass=your_password_here

---

### 2. k3s_setup.yml 파일 내용

---

- name: RHEL 8.1 기반 K3s HA 클러스터 구축 hosts: k3s_masters become: yes vars: k3s_token: "CMP_SECRET_TOKEN_2026" first_master_ip: "{{ hostvars[groups['k3s_masters'][0]]['ansible_host'] }}"
    
    tasks:
    
    - name: firewalld stop systemd: { name: firewalld, state: stopped, enabled: no }
        
    - name: selinux disable selinux: { state: disabled }
        
    - name: load kernel modules modprobe: { name: "{{ item }}", state: present } loop: [br_netfilter, overlay]
        
    - name: sysctl config sysctl: name: "{{ item.key }}" value: "{{ item.value }}" state: present sysctl_file: /etc/sysctl.d/k8s.conf loop:
        
        - { key: 'net.bridge.bridge-nf-call-iptables', value: '1' }
            
        - { key: 'net.bridge.bridge-nf-call-ip6tables', value: '1' }
            
        - { key: 'net.ipv4.ip_forward', value: '1' }
            
    - name: install packages yum: name: [tar, curl, iscsi-initiator-utils, nfs-utils] state: present
        
    - name: k3s leader init shell: | curl -sfL | K3S_TOKEN={{ k3s_token }} sh - s - server
        
        --cluster-init
        
        --write-kubeconfig-mode 644 when: inventory_hostname == groups['k3s_masters'][0]
        
    - name: k3s agent join shell: | curl -sfL | K3S_TOKEN={{ k3s_token }} sh - s - server
        
        --server https://{{ first_master_ip }}:6443
        
        --write-kubeconfig-mode 644 when: inventory_hostname != groups['k3s_masters'][0]
        
    - name: k3s start systemd: { name: k3s, state: started, enabled: yes }
        

---

### 3. 실행 방법 (리눅스 터미널)

파일 두 개를 만든 폴더 안에서 아래 명령어를 치면 됩니다.

**ansible-playbook -i inventory.ini k3s_setup.yml**

---

이제는 정말 잘 보이시죠? 이 코드는 RHEL 8.1에서 **Podman과 부딪히지 않게 K3s 전용 containerd를 쓰도록** 세팅되어 있습니다.

**"이 다음 단계로 Longhorn 스토리지까지 Ansible로 한 방에 깔아버리는 작업을 추가해 드릴까요?"**

---
이제 기술적인 도구들은 다 나왔습니다.

1. **Packer**: OVF 굽기 (기반 공사)
2. **Ansible**: K3s + Longhorn 세팅 (내부 인테리어)
3. **Helm**: 포털 + DB + Jenkins 배포 (가구 배치)


---


했던 작업들 

1.Local 에 Packer 설치
- Pakcer : 수동으로 OS 설치하는 게 아닌 자동으로 도와주는 설치 도우미
- 설정 파일 준비 : vsphere.pkr.hcl 
	- **vCenter 정보:** IP, 아이디, 비번
	- **리소스 정보:** VM을 생성할 호스트, 데이터스토어 이름
	- **OS 정보:** 사용할 Red Hat 8.1 ISO 파일의 경로
	- **Provisioner:** OS 설치 후 실행할 **그 Ansible 플레이북(`k3s_setup.yml`)**의 경로

2.Ansible
- **동작 방식:** Packer가 vSphere에 VM을 만들고 네트워크를 잡으면, 사용자 맥북에 있는 Ansible이 **SSH**를 타고 해당 VM에 접속해서 플레이북을 실행합니다.