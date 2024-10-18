![[Pasted image 20240808090854.png]]

pod is distributed walker node 
but it has a problem 

---

kubernetis is not just about pods
it also have label, deployment, statefulset, secret 

That is why management aspect has a difficulty 
namespace is a logical seperation unit 

![[Pasted image 20240808091159.png]]

---

but you should know what namespace is a logical seperation, not physical seperation 

namespace does not isolation 
namespace is a virtual space and group binding kubernetis object

---

### Namespace Purpose 

Individual Resource Specifying quotas

![[Pasted image 20240808091444.png]]

---

### By user namespace access rights 

Authorization 
ABAC or RBAC

APP을 조회함

1.dto.getTargetId를 이용해서 app을 가져옴
2.dto, app을 이용해서 deploymentRequest를 생성함
3.createDeploymentAppRequest 생성
4.RequestInfo 생성
5.requestInfo와 rolekey를 사용하여 isAutoApproval