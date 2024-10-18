
kubernetis를 배포하면 클러스터를 얻는다. 
쿠버네티스를 실행한다 = 클러스터를 실행하고 있다.
모든 클러스터는 최소 한 개 이상의 마스터 노드 및 워크 노드를 가진다.

쿠버네티스 클러스터는 두 가지 영역(컨트롤 플레인, 노드)로 구성되어 있다.
컨트롤 플레인 : Master Node 제어 영역
노드 : Worker Node라고 부른다. 애플리케이션 컨테이너를 실행하는 역할을 한다.


------

Master Node : 클러스터의 상태를 관리하고, 명령어를 처리하는 역할을 수행
- etcd, controller-manager, scheduler, kube api server라고 하는 여러 컴포넌트를 가진다.
- 3 tier 아키텍쳐 관계처럼 클라이언트 - 백엔드 - 데이터 서버 방식으로 노드가 돌아간다.
- scheduler, controller-manager가 클라이언트, kube api server가 백엔드, etcd가 데이터 서버에 해당한다.

---

scheduler :
- Api 서버와 통신하는 컴포넌트, 각각의 노드(워커 노드)의 자원 사용 상태(cpu, memory, gpu)를 관리한다.
- 아직 노드가 배정되지 않은 새로 생성된 pod를 감지하고 새로운 워크로드를 띄우는 역할
- 클러스터 내 자원할당이 가능한 노드중 알맞은 노드를 선택하여 해당 노드에 워크로드를 배포

controller-manager
- 여러 컨트롤러 프로세스 관리 - 크게 2가지로 나뉨 (Kube Controller-manager , Cloud Controller-manager)

---

- Cloud Controller-manager 대표적인 클라우드 provider(aws, gcp, azure)과 통신
- provider들의 종속적인 기능들을 클러스터에서 수행한다.

---
- Kube Controller Manager 
- Api 서버에는 다양한 리소스(pod, deployment, service, secret)이 있고 각각의 리소스들을 관리하는 컨트롤러가 배정된다.
- 이들이 api를 찌르면서 현재 클러스터 상태와, etcd 저장된 리소스의 상태를 비교한다.
- 만약 etcd 리소스 상태에 변화가 있다면 현재 클러스터 리소스에 반영함으로써 동기화
- 변화를 감지하고 동기화시키는 반복된 과정을 reconcile 

---

kube api server :
- 쿠버네티스 리소스와 클러스터의 상태 관리 및 동기화를 위한 API를 제공
- etcd를 데이터 저장소로 사용한다.

etcd :
- 분산 key-value 저장소로 클러스터의 상태를 저장한다.
- 만약 클러스터 상태를 백업하고 복구하고 싶다면 etcd만 건드리면 된다.
- 컨트롤 플레인 내부에 각각 할당된다.

---

워크로드 
- 클러스터에서 실행하려는 작업, 서비스, 프로세스 등을 가르키는 말로 사용된다.
- Pod 컨테이너 기반 애플리케이션의 최소 단위이지만 , Pod를 단독으로 생성하지는 않고, Deployment 또는 Job과 같은 API 리소스를 사용하여 생성한다.
- 워크로는 Pod 집합을 관리하여 Pod 집합이 지정된 개수만큼, 올바른 종류의 Pod가 실행될 수 있도록
- 보장하는 API 리소스 기반의 프로세스를 의미한다.

Deployment, ReplicaSet, StatefulSet, DaemonSet, Job, Crontab 등 다양한 API 리소스가 그 기반이 될 수 있다.
=> 정리하면 워크로드란, 쿠버네티스에서 실질적인 작업 리소스를 기반으로 구동되는 애플리케이션이라고 생각하면 된다.

----

API 리소스 

쿠버네티스가 관리할 수 있는 오브젝트의 종류라고 할 수 있다.
pod, service, configMap, secret 뿐만아니라, 클러스가 사용하는 node, serviceAccount,role도 리소스도 사용 된다.
객체지향으로 이해하자면 클래스이다.

-----

오브젝트

위의 API 리소스를 인스턴스화 한 것이다.
객체 지향으로 이해하면, 설계도를 통해 만들어낸 인스턴스 객체

---

API 리소스와 오브젝트간의 상호작용

1.오브젝트 명세가 API 서버로 전달
2.API 리소스 컨트롤러는 오브젝트 명세를 들어오면 API 리소스를 참고하여
오브젝트 인스턴스를 쉽게 만든다.
3.API 서버는 위 요청에 맞게 오브젝트 상태를 생성 및 업데이트
4.클러스터의 상태는 etcd 컴포넌트에서 관리하므로 etcd를 업데이트 한다.


- API 서버를 통해 새로운 커맨드를 감시
- API 서버를 통해 현재 클러스터 오브젝트 상태를 감시
---

- 쿠버네티스 오브젝트를 yml 기반 매니페스트 파일로 관리한다.
- apiVersion, kind, metadata, spec 이 대표적인 4가지 루트키
- apiVersion, kind, metadata는 반드시 존재하는 루트키
- spec은 API 리소스 종류에 따라 data, rules, subjects라는 다른 속성으로 대체되기도 한다.

configmap,secret -> data
role -> rules를 사용하는 리소스 

### required

apiVersion : 오브젝트가 어떤 API 그룹에 속하고 API 버전이 몇인지를 정의한다.
kind : 오브젝트가 어떤 API 리소스인지 타입을 정의한다.
metatdata : 오브젝트를 식별하기 위한 정보를 담는다.
spec : 오브젝트가 가지고자 하는 데이터를 정의한다. desired state(적용되길 원하는 오브젝트의 상태)

---

### Labels Annotations (optional)

모든 쿠버네티스 오브젝트는 Labels와 Annotations라는 메타데이터를 가질 수 있다.
Labels와 Annotations 모두 문자열 형식의 key-value 데이터를 기록한다.

Labels 
- 오브젝트를 식별
- 추후 검색, 분류, 필터링의 효율을 높이기 위해 사용
- Label Selector 기능은 특정 오브젝트를 필터링 하기 위한 목적

Annotations
- 식별이 아닌 다른 목적으로 사용
-  클러스터를 설정하는 여러 에드온 서비스가 존재하는데 어노테이션 값들을 자주 확인하여 오브젝트를 다룬다. 
- 애드온의 설정 용도로 사용될수도있고, 어떻게 처리할지의 용도로 사용될 수 있다.

---

k get pod --all-namespaces
